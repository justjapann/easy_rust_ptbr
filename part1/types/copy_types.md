## Copy types

Alguns tipos em Rust são muito simples. Eles são chamados de **copy types**. Esses tipos simples estão em toda a stack, e o compilador sabe o seu tamanho. Isso significa que eles são muito fáceis de copiar, então o compilador sempre vai copiar quando você o envia para uma função. Isso se da por que eles são tão pequenos e fáceis que não tem por que não o copiar. Então você não precisa se preucupar com quem é o dono desses tipos.

Esses tipos simples incluem: inteíros, floats, booleans (`true` e `false`), e `char`.

Como saber se o tipo **implements** copiou? (implements = pode usar) Você pode checar a documentação. Por exemplo, aqui está a documentação para char:

[https://doc.rust-lang.org/std/primitive.char.html](https://doc.rust-lang.org/std/primitive.char.html)

Na direita você pode ver **Trait Implementations**. Você pode ver o exemplo **Copy**, **Debug**, e **Display**. Então você sabe que um `char`:

- é copiado quando você envia ele a uma função (**Copy**)
- pode usar `{}` para printar (**Display**)
- pode usar `{:?}` para printar (**Debug**)

```rust
fn prints_number(number: i32) { // There is no -> so it's not returning anything
                             // If number was not copy type, it would take it
                             // and we couldn't use it again
    println!("{}", number);
}
fn main() {
    let my_number = 8;
    prints_number(my_number); // Prints 8. prints_number gets a copy of my_number
    prints_number(my_number); // Prints 8 again.
                              // No problem, because my_number is copy type!
}
```

Mas se você olhar a documentação para String, ela não copia o tipo.

[https://doc.rust-lang.org/std/string/struct.String.html](https://doc.rust-lang.org/std/string/struct.String.html)

Na direita de **Trait Implementations** você pode olhar a ordem alfabética. A, B, C... isso não **Copy** em C. Mas tem **Clone**. **Clone** é similar a **Copy**, mas normalmente a gente precisa de mais memória. Também, você tem que chamar com `.clone()` - por que ele não vai clonar sozinho.

No exemplo, `prints_country()` printa o nome do país, uma `String`. Nós queremos printar duas vezes, mas não podemos:

```rust
fn prints_country(country_name: String) {
    println!("{}", country_name);
}
fn main() {
    let country = String::from("Kiribati");
    prints_country(country);
    prints_country(country); // ⚠️
}
```

Vamos entender a mensagem.

```text
error[E0382]: use of moved value: `country`
 --> src\main.rs:4:20
  |
2 |     let country = String::from("Kiribati");
  |         ------- move occurs because `country` has type `std::string::String`, which does not implement the `Copy` trait
3 |     prints_country(country);
  |                    ------- value moved here
4 |     prints_country(country);
  |                    ^^^^^^^ value used here after move
```

A parte importante: `which does not implement the Copy trait`. Mas na documentação vimos que String implementa o traço `Clone`. Então nós podemos adicionar `.clone()` no seu código. Isso cria o clone, e envia o clone a função. Agora `country` continua vivo, e nós podemos usar ele.

```rust
fn prints_country(country_name: String) {
    println!("{}", country_name);
}
fn main() {
    let country = String::from("Kiribati");
    prints_country(country.clone()); // cria um clone e da ele a função. somente o clone vai, contry continua vivo
    prints_country(country);
}
```

Claro, se a `String` for muito longa, `.clone()` pode usar muita memória. Uma `String` pode ser um livro inteiro de tamanho, e toda vez que a gente chama `.clone()` ele vai copiar o livro. Então, usando `&` para a referência ser rápida, você pode fazer isso. Por exemplo, esse código envia `&str` em uma `String` e então faz um clone toda vez que é usado em uma função:

```rust
fn get_length(input: String) { // o dono da string
    println!("It's {} words long.", input.split_whitespace().count()); // divide para contar o numero de palavras
}
fn main() {
    let mut my_string = String::new();
    for _ in 0..50 {
        my_string.push_str("Here are some more words "); // push the words on
        get_length(my_string.clone()); // gives it a clone every time
    }
}
```

Isso printa:

```text
It's 5 words long.
It's 10 words long.
...
It's 250 words long.
```

São 50 clones. Aqui está usando uma referência, que é melhor:

```rust
fn get_length(input: &String) {
    println!("It's {} words long.", input.split_whitespace().count());
}
fn main() {
    let mut my_string = String::new();
    for _ in 0..50 {
        my_string.push_str("Here are some more words ");
        get_length(&my_string);
    }
}
```

Em vez de 50 clones, é zero.
