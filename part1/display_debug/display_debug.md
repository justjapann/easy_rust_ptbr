## Display e debug

**[Você pode ver esse capítulo no youtube](https://youtu.be/jd3pC248c0o)**

Variáveis simples podem ser printadas com `{}` dentro do `println!`, com exceção de algumas, então você precisa do **debug print**. Debug print é o print para programadores, porque ele te mostra mais informações. Debug as vezes pode não parecer bonito, mas ele tem informações extras para te ajudar.

Como você sabe se precisa usar `{:?}` e não `{}`? O compilador vai falar para você. Por exemplo:

```rust
fn main() {
    let doesnt_print = ();
    println!("This will not print: {}", doesnt_print); // ⚠️
}
```

Quando nós executamos isso, o compilador diz:

```text
error[E0277]: `()` doesn't implement `std::fmt::Display`
 --> src\main.rs:3:41
  |
3 |     println!("This will not print: {}", doesnt_print);
  |                                         ^^^^^^^^^^^^ `()` cannot be formatted with the default formatter
  |
  = help: the trait `std::fmt::Display` is not implemented for `()`
  = note: in format strings you may be able to use `{:?}` (or {:#?} for pretty-print) instead
  = note: required by `std::fmt::Display::fmt`
  = note: this error originates in a macro (in Nightly builds, run with -Z macro-backtrace for more info)
```

Isso é muita informação, mas a parte mais importante: `you may be able to use {:?} (or {:#?} for pretty-print) instead`. Isso quer dizer que você pode tentar usar `{:?}`, e também `{:#?}`

`{:#?}` é chamado de "pretty printing". É como um `{:?}`, mas ele printa com diferentes formatos com mais linhas.

Então Display significa printar com `{}`, e Debug printar com `{:?}`.

Mais uma coisa: você também pode usar `print!` sem `ln` se você não quer uma nova linha.

```rust
fn main() {
    print!("This will not print a new line");
    println!(" so this will be on the same line");
}
```

Isso printa `This will not print a new line so this will be on the same line`.
