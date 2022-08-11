## Giving references to functions

**Veja esse capítulo no Youtube: [referência imutável](https://youtu.be/mKWXt9YTavc) e [referência mutável](https://youtu.be/kJV1wIvAbyk)**

Referências são muito usadas em funções. A regra de valores em Rust é: o valor pode ter somente um dono.

Esse código não vai funcionar:

```rust
fn print_country(country_name: String) {
    println!("{}", country_name);
}
fn main() {
    let country = String::from("Austria");
    print_country(country); // printamos "Austria"
    print_country(country); // ⚠️ foi divertido, vamos fazer denovo!
}
```

Isso não funciona por que `country` é destroido. Aqui está como:

- Passo 1: Nós criamos uma `String` chamada `country`. `country` é o dono.
- Passo 2: Nós damos `country` a `print_country`. `print_country` não tem uma `->`, então ele não retorna nada. Depois `print_country` é finalizado, e `String` está morto agora.
- Passo 3: Nós tentamos dar `country` a `print_country`, mas já fizemos isso, não temos mais `country` para dar a algo.

Nós podemos fazer `print_country` devolver a `String`, mas isso é um pouco chato.

```rust
fn print_country(country_name: String) -> String {
    println!("{}", country_name);
    country_name // return it here
}
fn main() {
    let country = String::from("Austria");
    let country = print_country(country); // we have to use let here now to get the String back
    print_country(country);
}
```

Agora isso printa:

```text
Austria
Austria
```

A maneira muito melhor de arrumar isso é adicionando `&`.

```rust
fn print_country(country_name: &String) {
    println!("{}", country_name);
}
fn main() {
    let country = String::from("Austria");
    print_country(&country); // nos printamos "Austria"
    print_country(&country); // vamos fazer denovo!
}
```

Agora `print_country()` é uma funcão que faz referência a uma `String`: `&String`. Também, nós damos a referência a country escrevendo `&country`. Isso quer dizer "você pode olhar para ele, mas ainda é meu".

Agora vamos fazer algo semelhante com uma referência mutável. Aqui está um exemplo de como usa uma variável mutável.

```rust
fn add_hungary(country_name: &mut String) { // primeiro nos dizemos que a funcao pega a referencia mutavel
    country_name.push_str("-Hungary"); // push_str() adiciona um &str na String
    println!("Now it says: {}", country_name);
}
fn main() {
    let mut country = String::from("Austria");
    add_hungary(&mut country); // também precisamos dar uma referência mutável.
}
```

Isso printa `Now it says: Austria-Hungary`.

Então para concluir:

- `fn function_name(variable: String)` pega a `String` e vira dono dea. Se não retornar nada, a variável vai morrer dentro da função.
- `fn function_name(variable: &String)` empresta uma `String` e pode olhar para ela
- `fn function_name(variable: &mut String)` empresta uma `String` e pode mudar ela

Aqui está um exemplo que parece uma referência mutável, mas é diferente.

```rust
fn main() {
    let country = String::from("Austria"); // country nao é mutavel, mas vamos printar Austria-Hungary. Como?
    adds_hungary(country);
}
fn adds_hungary(mut country: String) { // Aqui está como: adds_hungary pega a String e declara como mutavel!
    country.push_str("-Hungary");
    println!("{}", country);
}
```

Como isso é possível? Por que `mut country` não é uma referência: `adds_hungary` possui `country` agora. (lembre, ela leva `String` e não `&String`). No momento que você chama `adds_hungary`, ela passa a ser dono completo. `country` não tem mais nada a ver com `String::from("Austria")`. Então `adds_hungary` pode tornar `country` como mutável e é perfeitamente seguro fazer isso.

Se lembra da situação do funcionário e do gerente acima? Nesta situação, é como se o funcionário entregasse todo o computador ao gerente. O funcionário nunca mais vai tocar nele denovo, então o gerente pode fazer o que quiser.
