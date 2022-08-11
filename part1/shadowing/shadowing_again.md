### Shadowing denovo

Lembra quando nós dissemos que shadowing não **destroi** o valor, mas o **bloqueia**? Agora podemos usar referências para ver isso.

```rust
fn main() {
    let country = String::from("Austria");
    let country_ref = &country;
    let country = 8;
    println!("{}, {}", country_ref, country);
}
```

Isso printa `Austria, 8` ou `8, 8`? Printa `Austria, 8`. Primeiro nós declaramos `String` chamada `country`. Em seguida nós criamos a referência `country_ref` para essa string. Então nós cobrimos country com 8, que é um `i32`. Mas o primeiro `country` não foi ,destruido, então `country_ref` ainda é "Austria", não "8". Aqui está o mesmo código com alguns comentários de como isso funciona:

```rust
fn main() {
    let country = String::from("Austria"); // agora nos temos uma string chamada country
    let country_ref = &country; // country_ref é a referencia para esse valor. Ela nao vai mudar
    let country = 8; // agora nos temos a variavel chamada country que é um i8. Mas ela nao tem realacao com a outra acima, ou com country_ref
    println!("{}, {}", country_ref, country); // country_ref continua se referindo ao valor de String::from("Austria") que foi lhe dado.
}
```
