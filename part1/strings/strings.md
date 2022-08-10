## Strings

**[Você pode ver esse capítulo no Youtube](https://youtu.be/pSyaGzGg26o)**

Rust tem dois tipos de strings principais: `String` e `&str`. Qual a diferença entre eles?

- `&str` é uma simples string. Quando você escreve `let my_variable = "Hello, world!"`, você cria uma `&str`. A `&str` é muito rápida.
- `String` é uma string mais complicada, ela é um pouco mais lenta, porém ela tem mais funções. A `String` é um pointer, com dados no heap.

Outra coisa é que a `&str` tem o `&` na frente dele por que precisa de uma referência para usar um `str`. Isso é por conta do que vimos acima: o stack precisa saber do tamanho, então nós damos o `&` que sabe o tamanho e ele fica feliz. Além disso, por você usar `&` para interagir com o `str`, você não possui ele. Mas a `String` é um _owned_ type, nós vamos aprender sobre isso mais tarde por que é importante que você saiba.

Ambos `&str` e `String` são UTF-8. Por exemplo, você pode escrever:

```rust
fn main() {
    let name = "서태지"; // isso é um nome coreano. Sem problemas, por que o &str é UTF-8.
    let other_name = String::from("Adrian Fahrenheit Țepeș"); // Ț e ș não tem problemas em UTF-8.
}
```

Você poder ver em `String::from("Adrian Fahrenheit Țepeș")` que é fácil criar uma `String` com um `&str`. Os dois tipos estão muito ligados entre si, mesmo sendo diferentes.

Você pode escrever simples emojis, obrigado UTF-8.

```rust
fn main() {
    let name = "😂";
    println!("My name is actually {}", name);
}
```

No seu computador vai printar `My name is actually 😂` a menos que sua linha de comando não possa imprimi-lo, então vai aparecer `My name is actually �`. Mas Rust não tem problemas com emojis ou outro Unicode.

Vamos ver a razão para usar `&` no `str` para ter certeza que entendemos.

- `str` é um tipo de tamanho dinâmico (tamanho dinâmico = o tamanho pode ser diferente). Por exemplo, os nomes "서태지" e "Adrian Fahrenheit Țepeș" não são do mesmo tamanho:

```rust
fn main() {
    println!("A String is always {:?} bytes. It is Sized.", std::mem::size_of::<String>()); // std::mem::size_of::<Type>() da o tamanho em bytes de um tipo
    println!("And an i8 is always {:?} bytes. It is Sized.", std::mem::size_of::<i8>());
    println!("And an f64 is always {:?} bytes. It is Sized.", std::mem::size_of::<f64>());
    println!("But a &str? It can be anything. '서태지' is {:?} bytes. It is not Sized.", std::mem::size_of_val("서태지")); // std::mem::size_of_val() da o tamanho em bytes de uma variável
    println!("And 'Adrian Fahrenheit Țepeș' is {:?} bytes. It is not Sized.", std::mem::size_of_val("Adrian Fahrenheit Țepeș"));
}
```

Isso printa:

```text
A String is always 24 bytes. It is Sized.
And an i8 is always 1 bytes. It is Sized.
And an f64 is always 8 bytes. It is Sized.
But a &str? It can be anything. '서태지' is 9 bytes. It is not Sized.
And 'Adrian Fahrenheit Țepeș' is 25 bytes. It is not Sized.
```

É por isso que precisamos de um &, por causa que o `&` cria um pointer, e Rust sabe o tamanho do pointer. Então o pointer vai no stack. Se nós escrevermos `str`, Rust não vai saber oque fazer por que não sabe seu tamanho.

Tem muitas maneiras de fazer uma `String`. Aqui estão alguns:

- `String::from("This is the string text");` Esse é um método da String que pega um textp e cria uma String.
- `"This is the string text".to_string()`. Esse é um método do &str que cria uma String.
- O `format!` macro é como um `println!`, exceto que cria uma string, ao invés de printar. Então você pode fazer:

```rust
fn main() {
    let my_name = "Billybrobby";
    let my_country = "USA";
    let my_home = "Korea";
    let together = format!(
        "I am {} and I come from {} but I live in {}.",
        my_name, my_country, my_home
    );
}
```

Agora a gente tem uma string chamada _together_, mas ainda não printa nada.

Outro jeito de criar uma string é chamando `.into()`, mas ele é um pouco diferente por que `.into()` não é so para criar uma `String`. Outros tipos podem ser facilmente convertidos para outro tipo com `From` e `.into()`. E se você tem `From`, então você também tem um `.into()`. `From` é mais claro por que você sempre vai saber o tipo: você sabe que `String::from("Some str")` é uma `String` para `&str`. Mas com `.into()`, o compilador pode não saber disso:

```rust
fn main() {
    let my_string = "Try to make this a String".into(); // ⚠️
}
```

Rust não sabe o tipo que você quer, por que muitos tipos podem ser feitos de `&str`. Isso quer dizer, "Eu posso criar um &str em um monte de coisas. qual deles você quer?"

```text
error[E0282]: type annotations needed
 --> src\main.rs:2:9
  |
2 |     let my_string = "Try to make this a String".into();
  |         ^^^^^^^^^ consider giving `my_string` a type
```

Então você pode fazer:

```rust
fn main() {
    let my_string: String = "Try to make this a String".into();
}
```

E agora você pega a string

#### [Proximo capítulo](https://github.com/justjapann/easy_rust_ptbr/blob/main/part1/const_static/const_static.md)
