## Tuplas
**[Você pode ver esse capítulo no youtube](https://youtu.be/U67Diy6SlTg)**

Tuplas em Rust usam `()`. Já vimos muitas tuplas vazias, isso por que *nothing* em uma função significa uma tupla vazia.

```text
fn do_something() {}
```

Isso é o mesmo resumido que:

```text
fn do_something() -> () {}
```

A função não recebe nada(uma tupla vazia), e retorna *nothing*. Portanto, já usamos muitas tuplas. Quando você não retorna nada em uma função, você nada verdade esta retornando uma tupla vazia.  

```rust
fn just_prints() {
    println!("I am printing"); // estamos retornando uma tupla vazia
}
fn main() {}
```

Mas tuplas poder conter muitas coisas, e ter diferentes tipos também. itens dentro da tupla também são indexados com números 0, 1, 2, etc. Mas para acessa-lós, você usa `.` em vez de `[]`. Vamos colocar um monte de tipos em uma tupla para ver oque acontece.

```rust
fn main() {
    let random_tuple = ("Here is a name", 8, vec!['a'], 'b', [8, 9, 10], 7.7);
    println!(
        "Inside the tuple is: First item: {:?}
Second item: {:?}
Third item: {:?}
Fourth item: {:?}
Fifth item: {:?}
Sixth item: {:?}",
        random_tuple.0,
        random_tuple.1,
        random_tuple.2,
        random_tuple.3,
        random_tuple.4,
        random_tuple.5,
    )
}
```

Isso printa:

```text
Inside the tuple is: First item: "Here is a name"
Second item: 8
Third item: ['a']
Fourth item: 'b'
Fifth item: [8, 9, 10]
Sixth item: 7.7
```

Essa tupla é tipo do tipo `(&str, i32, Vec<char>, char, [i32; 3], f64)`.

Você pode usar as tuplas para criar múltiplas variáveis. Olhe esse código:

```rust
fn main() {
    let str_vec = vec!["one", "two", "three"];
}
```

`str_vec` tem três itens dentro dele. E se nós quisermos retirar um item dentro dele? É ai que usamos as tuplas.

```rust
fn main() {
    let str_vec = vec!["one", "two", "three"];
    let (a, b, c) = (str_vec[0], str_vec[1], str_vec[2]);
    println!("{:?}", b);
}
```

Isso printa `"two"`(no caso, o "b"). Isso é chamado de *destructuring*, isso porque a primeiro as variáveis estão dentro da estrutura, mas depois chamamos elas de `a`, `b`, e `c` fora da estrutura.

Se você quer desestruturar, mas não quer perder todas as variáveis, você pode usar `_`.

```rust
fn main() {
    let str_vec = vec!["one", "two", "three"];
    let (_, _, variable) = (str_vec[0], str_vec[1], str_vec[2]);
}
```

Agora nós criamos somente a variável chamada `variable`, e não para todos os outros como antes.

Existem muitos outros collection types, tuplas, vecs e arrays. Nós vamos aprender sobre eles mais tarde. Primeiro, vamos dar uma olhada no Fluxo de controle.