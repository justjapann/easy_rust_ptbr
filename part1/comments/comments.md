## Comentários

**[Você pode ver esse capítulo no youtube](https://youtu.be/fJ7jBZG_Rpo)**

Comentários são feitos para programadores lerem, não para o computador. É bom escrever comentários para outras pessoas lerem e entenderem seu código, isso também é uma boa maneira de ler e entender seu código mais tarde, caso precise, (Muitas pessoas escrevem bons códigos, mas esquecem o que eles podem fazer). Para escrever comentários em Rust você pode usar `//`:

```rust
fn main() {
    // Um programa em Rust começa com a fn main()
    // Você coloca seu código dentro do bloco, ele começa com { e termina com }
    let some_number = 100; // Nós podemos escrever quantos comentários quisermos, o computador nunca vai executa-lós.
}
```

Quando você colocar esse sinal `//`, o compilador não vai olhar nada à direita dele.

Há outro tipo de comentário que você pode fazer escrevendo `/*` no começo e `*/` no final. Isso pode ser bom para escrever no meio do seu código.

```rust
fn main() {
    let some_number/*: i16*/ = 100;
}
```

Para o compilador, `let some_number/*: i16*/ = 100;` se parece com `let some_number = 100;`.

O `/* */` pode ser muito útil para comentários grandes que ocupam mais de uma linha. Nesse exemplo você pode perceber que vai precisar escrever `//` em todas as linahs. Mas se você colocar `/*`, ele não vai finalizar até encontrar o `*/`.

```rust
fn main() {
    let some_number = 100; /* Deixe eu te falar um pouco
    sobre esse número.
    100, meu número favotiro.
    Ele é chamado de some_number, mas na verdade eu acho que... */
    let some_number = 100; // Deixe eu te falar um pouco
    // sobre esse número.
    // It's 100, which is my favourite number.
    // Ele é chamado de some_number, mas na verdade eu acho
    // que ..
}
```

#### [Proximo capítulo](https://github.com/justjapann/easy_rust_ptbr/blob/main/part1/types/types.md)
