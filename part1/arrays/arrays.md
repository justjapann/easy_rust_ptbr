### Arrays

Um array são um conjunto de dados dentro de um quadrado de chaves: `[]`.
Arrays:

- Não deve mudar de tamanho,
- Deve conter apenas o mesmo tipo.

Eles são muito rápidos, entretanto:

O tipo de um array é: `[type; number]`. Por exemplo, o tipo de `["One", "Two"]` é `[&str; 2]`. Isso significa que esses dois arrays têm tipos diferentes:

```rust
fn main() {
    let array1 = ["One", "Two"]; // isso tem o tipo [&str; 2]
    let array2 = ["One", "Two", "Five"]; // mas esse tem o tipo [&str; 3]. tipos diferentes!
}
```

Uma boa dica: para saber o tipo de uma variável, você pode perguntar ao compilador dando instruções ruins. Por exemplo:

```rust
fn main() {
    let seasons = ["Spring", "Summer", "Autumn", "Winter"];
    let seasons2 = ["Spring", "Summer", "Fall", "Autumn", "Winter"];
    seasons.ddd(); // ⚠️
    seasons2.thd(); // ⚠️ também
}
```

O compilador fala, "O que? Não existe o método `.ddd()` para as seasons e também não existe o método `.thd()` para as seasons2!!" como você pode ver:

```text
error[E0599]: no method named `ddd` found for array `[&str; 4]` in the current scope
 --> src\main.rs:4:13
  |
4 |     seasons.ddd(); //
  |             ^^^ method not found in `[&str; 4]`
error[E0599]: no method named `thd` found for array `[&str; 5]` in the current scope
 --> src\main.rs:5:14
  |
5 |     seasons2.thd(); //
  |              ^^^ method not found in `[&str; 5]`
```

Então ele fala pra você `` method not found in `[&str; 4]` ``, que é o tipo.

Se você quer um array com o mesmo valor, pode declarar ele assim:

```rust
fn main() {
    let my_array = ["a"; 10];
    println!("{:?}", my_array);
}
```

Isso printa `["a", "a", "a", "a", "a", "a", "a", "a", "a", "a"]`.

Esse método é usado para criar vários buffers. Por exemplo, `let mut buffer = [0; 640]` cria um array com 640 zeros. Então podemos mudar o zero para outros números para adicionar dados.

Você pode indexar (pegar) entradas em um array com []. O primeiro valor é [0], o segundo [1], assim por diante.

```rust
fn main() {
    let my_numbers = [0, 10, -20];
    println!("{}", my_numbers[1]); // printa 10
}
```

Você pode pegar uma fatia(um pedaço) de um array. Primeiro você precisa de &, por que o compilador não sabe seu tamanho. Então você pode usar `..` para mostrar a distância.

Por exemplo, vamos o array: `[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]`.

```rust
fn main() {
    let array_of_ten = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
    let three_to_five = &array_of_ten[2..5];
    let start_at_two = &array_of_ten[1..];
    let end_at_five = &array_of_ten[..5];
    let everything = &array_of_ten[..];
    println!("Three to five: {:?}, start at two: {:?}, end at five: {:?}, everything: {:?}", three_to_five, start_at_two, end_at_five, everything);
}
```

Lembre-se que:

- Números de index começam em 0 (não 1)
- Distâncias de index são **exclusivos** (eles não incluem o último número)

Então `[0..2]` significa o primeiro e segundo número (0 e 1). Ou você pode chamar de "zero e primeiro" index. Não tem o terceiro item, que é o index 2.

Você também pode ter um **inclusive** range, que também inclui o último número. Para fazer isso, adicione `=` para escrever `..=`, em vez de `..`. Então, em vez de `[0..2]`, você pode escrever `[0..=2]` se quiser o primeiro, segundo e terceiro item.
