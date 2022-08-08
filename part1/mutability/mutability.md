## Mutabilidade (mudança)

**[Você pode ver esse capítulo no youtube](https://youtu.be/Nyyd6qn7dZY)**

Quando você declara uma variável com `let`, ela é imutável (não pode sofrer mudanças).

Isso não vai funcionar:

```rust
fn main() {
    let my_number = 8;
    my_number = 10; // ⚠️
}
```

O compilador vai dizer: `error[E0384]: cannot assign twice to immutable variable my_number`. Isso é por que as variáveis são imutáveis se você apenas escrever `let`.

Mas as vezes você quer trocar o valor da sua variável. Para fazer uma variável mutavel, adicione `mut` depois de `let`:

```rust
fn main() {
    let mut my_number = 8;
    my_number = 10;
}
```

Agora ele não vai dar nenhum problema.

No entando, você não pode trocar o tipo: mesmo usando `mut` você não consegue isso.

Isso não funciona:

```rust
fn main() {
    let mut my_variable = 8; // it is now an i32. That can't be changed
    my_variable = "Hello, world!"; // ⚠️
}
```

Você verá a mesma mensagem "expected" do compilador: `expected integer, found &str`. `&str` isso é um tipo de string que veremos mais tarde.
