## Printando 'hello, world!'

**Você pode ver esse capítulo no youtube: [Video 1](https://youtu.be/yYlPHRl2geQ), [Video 2](https://youtu.be/DTCSfBJJZb8)**

Quando você começar com um novo programa em Rust, ele sempre vai ter esse código:

```rust
fn main() {
    println!("Hello, world!");
}
```

- `fn` significa função,
- `main` é uma função que inicia seu programa,
- `()` significa que não damos nenhuma variável a função para iniciar.

`{}` é chamado de **bloco do código**. Nesse espaço é onde fica nosso código.

`println!` é um **macro** que printa no console. O **macro** é como uma função que escreve o código para você. Macros tem um `!` depois deles. Nós vamos aprender mais sobre macros mais tarde. Por agora, lembre do `!` que fala que isso é um macro.

Para aprender sobre o `;`, nós vamos criar outra função. Primeiro, na `main` vamos printar o número 8:

```rust
fn main() {
    println!("Hello, world number {}!", 8);
}
```

O `{}` na `println!` significa "pegue a variável e coloque aqui". Isso printa `Hello, world number 8!`.

Podemos colocar mais, igual fizemos anteriormente:

```rust
fn main() {
    println!("Hello, worlds number {} and {}!", 8, 9);
}
```

Isso printa `Hello, worlds number 8 and 9!`.

Agora, vamos criar uma função.

```rust
fn number() -> i32 {
    8
}
fn main() {
    println!("Hello, world number {}!", number());
}
```

Isso também printa `Hello, world number 8!`. QUando Rust olha o `number()` ele vê uma função. Essa função:

- Não vai receber nada (because it has `()`)
- Retorna um `i32`. O `->` (Chamada de "skinny arrow") mostra oque a função vai retornar.

Dentro da função a gente tem apenas um `8`. Porque não tem um `;`, esse é o valor que retorna. Se tiver um `;`, não retornaria nada (ele deve retornar uma `()`). Rust não vai compilar se tiver um `;`, por que ele retorna um `i32` e `;` retorna uma `()`, e não `i32`:

```rust
fn main() {
    println!("Hello, world number {}", number());
}
fn number() -> i32 {
    8;  // ⚠️
}
```

```text
5 | fn number() -> i32 {
  |    ------      ^^^ expected `i32`, found `()`
  |    |
  |    implicitly returns `()` as its body has no tail or `return` expression
6 |     8;
  |      - help: consider removing this semicolon
```

Isso significa "Você me disso um `number()` que retorna um `i32`, mas você adicionou um `;` que não retorna nada". Então o compilador sugere você retirar a semi-coluna.

Você também pode escrever `return 8;` mas em Rust é comum você so remover a `;` do `return`.

Quando você quer dar uma variável a uma função, informe ela dentro do `()`. Você precisa dar um nome e um tipo a ela.

```rust
fn multiply(number_one: i32, number_two: i32) { // dois i32s vao entrar na funcao. vamos chamar eles de number_one e number_two.
    let result = number_one * number_two;
    println!("{} times {} is {}", number_one, number_two, result);
}
fn main() {
    multiply(8, 9); // Damos os numeros a funcao direto
    let some_number = 10; // ou declaramos duas variaveis com eles
    let some_other_number = 2;
    multiply(some_number, some_other_number); // e colocamos elas na funcao
}
```

Nós também podemos retornar `i32`. apenas retire a semi-coluna no final:

```rust
fn multiply(number_one: i32, number_two: i32) -> i32 {
    let result = number_one * number_two;
    println!("{} times {} is {}", number_one, number_two, result);
    result // retorna i32 que pedimos
}
fn main() {
    let multiply_result = multiply(8, 9); // retorna uma funcao
}
```

#### [Proximo capítulo](https://github.com/justjapann/easy_rust_ptbr/blob/main/part1/print_helloWorld/variable.md)
