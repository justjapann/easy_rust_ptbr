## Inferência de tipos

**[Você pode ver esse capítulo no youtube](https://youtu.be/q1D2vpy3kEI)**

Inferência de tipos significa que se você não informar ao compilador o tipo, ele decide por ele mesmo. O compilador sempre vai precisar saber o tipo das variáveis, mas você nem sempre precisa informar quais são, na verdade, você não precisa dizer para ele. Por exemplo, para `let my_number = 8`, `my_number` tem um tipo `i32`, isso é por que o compilador escolhe i32 para inteiros se você não dizer para ele. Mas se você dizer `let my_number: u8 = 8`, ele vai colocar `my_number` como `u8`, por que você informou `u8`.

Geralmente o compilador pode advinhar, mas as vezes você vai precisar informar o tipo a ele, por duas razões:

1. Você está fazendo algo muito complexo e o compilador não consegue advinhar o tipo que você quer.
2. Você quer um tipo diferente (por exemplo, você quer `i128`, não um `i32`).

Para especificar o tipo, adicione dois pontos `:` depois do nome da variável.

```rust
fn main() {
    let small_number: u8 = 10;
}
```

Para números, você pode dizer o tipo depois do número. você não precisa dar espaço - so colocar o tipo depois do número.

```rust
fn main() {
    let small_number = 10u8; // 10u8 = 10 com tipo u8
}
```

Você também pode adicionar `_` se quiser tornar seu número fácil de ler.

```rust
fn main() {
    let small_number = 10_u8; // Isso é facil de ler
    let big_number = 100_000_000_i32; // 100 milhoes de vezes mais facil de ler com _
}
```

O `_` não muda nada no número, ele apenas torna mais fácil de o ler. E não importa quantos `_` você usa:

```rust
fn main() {
    let number = 0________u8;
    let number2 = 1___6______2____4______i32;
    println!("{}, {}", number, number2);
}
```

Isso printa `0, 1624`.

#### [Proximo capítulo](https://github.com/justjapann/easy_rust_ptbr/blob/main/part1/type_inference/float.md)
