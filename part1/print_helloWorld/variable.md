### Declarando variáveis e bloco de códigos

Use `let` para declarar uma variável (declarar uma variável = falar a Rust para criar uma variável).

```rust
fn main() {
    let my_number = 8;
    println!("Hello, number {}", my_number);
}
```

Variáveis começam e terminam em um bloco de código `{}`. Nesse exemplo, `my_number` termina antes que chamamos `println!`, por que ele está dentro do seu bloco do código.

```rust
fn main() {
    {
        let my_number = 8; // my_number comeca aqui
                           // my_number termina aqui!
    }
    println!("Hello, number {}", my_number); // ⚠️ nao tem my_number e
                                             // println!() nao consegue achar ele
}
```

Você pode usar o bloco de código para retornar o valor:

```rust
fn main() {
    let my_number = {
    let second_number = 8;
        second_number + 9 // sem semi-coluna, entao o bloco retorna 8 + 9.
                          // isso funciona como uma funçao
    };
    println!("My number is: {}", my_number);
}
```

Se você adicionar uma semi-coluna dentro do bloco, ele vai retornar `()` (nada):

```rust
fn main() {
    let my_number = {
    let second_number = 8; // declara second_number,
        second_number + 9; // adiciona 9 em second_number
                           // mas ele nao retorna!
                           // second_number esta morto agora
    };
    println!("My number is: {:?}", my_number); // my_number é ()
}
```

Então por que nós escrevemos `{:?}` e não `{}`? Nós vamos falar sobre isso agora.
