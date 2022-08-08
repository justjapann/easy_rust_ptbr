### Floats

Floats são números com pontos decimais. 5.5 é um float, e 6 é um inteiro. 5.0 também é um float, até 5. é um float.

```rust
fn main() {
    let my_float = 5.; // Rust vê, e sabe que isso é um float
}
```

Mas os tipos não são chamados de `float`, eles são chamados de `f32` e `f64`. Isso é o mesmo que os inteiros: os números depois de `f` mostra a quantidade de bits. Se você não quer escrever o tipo, Rust vai escolher `f64`.

Claro, somente floats com o mesmo tipo podem ser usados juntos, então você não pode adicionar `f32` em um `f64`.

```rust
fn main() {
    let my_float: f64 = 5.0; // Isso é um f64
    let my_other_float: f32 = 8.5; // Isso é um f32
    let third_float = my_float + my_other_float; // ⚠️
}
```

Quando você tentar executar isso, Rust vai dizer:

```text
error[E0308]: mismatched types
 --> src\main.rs:5:34
  |
5 |     let third_float = my_float + my_other_float;
  |                                  ^^^^^^^^^^^^^^ expected `f64`, found `f32`
```

O compilador escreve "expected (type), found (type)" quando você usa um tipo errado. Ele lê seu código assim:

```rust
fn main() {
    let my_float: f64 = 5.0; // O compilador vê um f64
    let my_other_float: f32 = 8.5; // o compilador ve um f32. um tipo diferente.
    let third_float = my_float + // se voce quer adicionar my_float em algo, entao use f64 com outr f64. agora ele espera um f64...
    let third_float = my_float + my_other_float;  // ⚠️ mas isso encontra um f32. entao nao podem ser adicionados juntos.
}
```

Então quando você vê "expected (type), found (type)", você deve encontar por que o compilador espera um tipo diferente.

Claro, com simples números isso é fácil de arrumar. você pode converter `f32` para `f64` com `as`:

```rust
fn main() {
    let my_float: f64 = 5.0;
    let my_other_float: f32 = 8.5;
    let third_float = my_float + my_other_float as f64; // my_other_float é f64 = use my_other_float como um f64
}
```

Ou para ser mais simples, remova as declarações dos tipos. ("declarar um tipo" = "dizer a Rust para usar esse tipo") Rust vai escolher os tipos que podem ser usados juntos.

```rust
fn main() {
    let my_float = 5.0; // Rust vai escolher f64
    let my_other_float = 8.5; // denovo vai escolher f64
    let third_float = my_float + my_other_float;
}
```

O compilador de Rust é inteligente e não vai escolher f64 se você precisar de um f32:

```rust
fn main() {
    let my_float: f32 = 5.0;
    let my_other_float = 8.5; // normalmente rust vai escolher f64,
    let third_float = my_float + my_other_float; // mas agora ele sabe que voce precisa adicionar com um f32. entao ele escolhe um f32 para my_other_float tambem
}
```
