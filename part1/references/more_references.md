## Mais sobre referências

**[Você pode ver esse capítulo no youtube](https://youtu.be/R13sQ8SNoEQ)**

Referências são muito importantes em Rust. Rust usa referências para garantir que o acesso a memória está seguro. Nós já sabemos que usamos `&` para criar uma referência:

```rust
fn main() {
    let country = String::from("Austria");
    let ref_one = &country;
    let ref_two = &country;
    println!("{}", ref_one);
}
```

Isso printa `Austria`.

No código, `country` é uma `String`. Então criamos duas referências para `country`. Elas tem o tipo `&String`, que você pode dizer como "referência a string". Nós poderiamos criar três referências ou cem referências para `country` que isso não seria um problema.

Mas isso é um problema:

```rust
fn return_str() -> &str {
    let country = String::from("Austria");
    let country_ref = &country;
    country_ref // ⚠️
}
fn main() {
    let country = return_str();
}
```

A função `return_str()` cria uma string, em seguida, cria uma referência para a string, depois tenta retornar com a referência. Mas a string `country` so fica viva dentro da função, e depois morre. Uma vez que uma variável se foi, o computador vai limpar a memória e usá-la para outra coisa. Depois que a função acabou, `country_ref` está se referindo a uma memória morta, e isso não é bom. Rust nos impede de cometer um erro com a memoria aqui.

Isso é uma parte muito importante sobre "owned" type, que falamos acima. Por que você tem uma `String`, e você pode passar ao redor dela, mas a `&String` vai morrer se a `String` morrer, então você não vai conseguir passar a "ownership" para ele.

#### [Proximo capítulo](https://github.com/justjapann/easy_rust_ptbr/blob/main/part1/references/mutable_references.md)
