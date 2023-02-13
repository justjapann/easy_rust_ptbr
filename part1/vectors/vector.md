## Vectors

**[Você pode ver esse capítulo no Youtube](https://youtu.be/Eh-DsRnDKmw)**

Do mesmo jeito que temos `&str` e `String`, nós temos arrays e vectors. Arrays são rápidos mas com menos funcionalidades, e vectors são lentos com mais funcionalidades. (Claro, Rust é sempre rápido e vectors não são tão lentos assim, apenas lentos comparados a arrays.) O tipo é escrito de `Vec`, e você pode chamar também de "vec".

Existem duas maneiras principais de criar um Vector. A primeira é tipo `String` usando `new`:

```rust
fn main() {
    let name1 = String::from("Windy");
    let name2 = String::from("Gomesy");
    let mut my_vec = Vec::new();
    // se voce executar o programa agora, o compilador vai nos dar um erro.
    // ele nao sabe o tipo do Vec.
    my_vec.push(name1); // agora ele sabe: é Vec<String>
    my_vec.push(name2);
}
```

Você pode ver que `Vec` sempre vai ter algo dentro dele, e pra isso que o `<>` (angle brackets) server. Um `Vec<String>` é um vector com uma ou mais `String`s. Você pode ter mais de um tipo dentro. Por exemplo:

- `Vec<(i32, i32)>` isso é um `Vec` que tem um item com uma tupla: `(i32, i32)`.
- `Vec<Vec<String>>` isso é um `Vec` que tem um `Vec`s de `Strings`. Vamos supor que você quer salvar seu livro favorito como `Vec<String>`. Então você faz isso novamente com outro livro, e obtém outro `Vec<String>`. Para armazenar os dois livros, você os colocaria em outro `Vec` e isso seria um `Vec<Vec<String>>`.

Em vez de usar `.push()` para fazer Rust decidir o tipo, você pode declarar ele.

```rust
fn main() {
    let mut my_vec: Vec<String> = Vec::new(); // O compilador sabe o tipo
                                              // entao isso nao da erro.
}
```

Você pode ver que os itens dentro do vector tem o mesmo tipo.

Outra maneira fácil de criar um vector é com o macro `vec!`. Ele se parece com uma declaração de array, mas tem `vec!` na frente dele.

```rust
fn main() {
    let mut my_vec = vec![8, 10, 10];
}
```

O tipo é `Vec<i32>`. Você pode chamar de "Vec de i32s", o `Vec<String>` de "Vec de strings", e o `Vec<Vec<String>>` de "Vec de um vec de strings".

Você pode cortar o vector também, assim como no array.

```rust
fn main() {
    let vec_of_ten = vec![1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
    // Tudo é o mesmo que acima, exceto que adicionamos vec!.
    let three_to_five = &vec_of_ten[2..5];
    let start_at_two = &vec_of_ten[1..];
    let end_at_five = &vec_of_ten[..5];
    let everything = &vec_of_ten[..];
    println!("Three to five: {:?},
start at two: {:?}
end at five: {:?}
everything: {:?}", three_to_five, start_at_two, end_at_five, everything);
}
```

Por o vec ser mais lento que um array, nós podemos usar alguns métodos para deixá-lo mais rápido. Um vec tem a **capacity**, que significa o espaço dado a um vector. Quando você da um novo item ao vector, ele se aproxima cada vez mais da capacidade. Então, se você ultrapassar a capacidade, ele dobrará sua capacidade e copiará os itens para o novo espaço. Isso é chamado de realocação. Nós vamos usar um método chamado `.capacity()` para olhar a capacidade de um vector à medida que adicionamos itens a ele.

Por exemplo:

```rust
fn main() {
    let mut num_vec = Vec::new();
    println!("{}", num_vec.capacity()); // 0 elementos: printa 0
    num_vec.push('a'); // adiciona um character
    println!("{}", num_vec.capacity()); // 1 elemento: printa 4. Vecs com 1 item sempre começa com 4 de capacidade
    num_vec.push('a'); // adiciona mais 1
    num_vec.push('a'); // adiciona mais 1
    num_vec.push('a'); // adiciona mais 1
    println!("{}", num_vec.capacity()); // 4 elementos: continua printando 4.
    num_vec.push('a'); // adiciona mais 1
    println!("{}", num_vec.capacity()); // printa 8. Nos temos 5 elementos, mas dobrou de 4 para 8 para abrir espaço
}
```

Isso printa:

```text
0
4
4
8
```

Então esse vector tem 2 realocações: 0 para 4, e 4 para 8. Nós podemos deixar isso mais rápido:

```rust
fn main() {
    let mut num_vec = Vec::with_capacity(8); // Give it capacity 8
    num_vec.push('a'); // add one character
    println!("{}", num_vec.capacity()); // prints 8
    num_vec.push('a'); // add one more
    println!("{}", num_vec.capacity()); // prints 8
    num_vec.push('a'); // add one more
    println!("{}", num_vec.capacity()); // prints 8.
    num_vec.push('a'); // add one more
    num_vec.push('a'); // add one more // Now we have 5 elements
    println!("{}", num_vec.capacity()); // Still 8
}
```

Esse vector tem 0 realocações, que é melhor. Então, se você acha que sabe quantos elementos você precisa, você pode usar `Vec::with_capacity()` para deixar isso mais rápido.

Você lembra que usamos `.into()` para transformar um `&str` em `String`. Você também pode usá-lo para transformar um array em um `Vec`. Você tem que dizer `.into()` que quer um `Vec`, mas você não precisa escolher o tipo de `Vec`. Se você não quiser escolher, você pode escrever `Vec<_>`.

```rust
fn main() {
    let my_vec: Vec<u8> = [1, 2, 3].into();
    let my_vec2: Vec<_> = [9, 0, 10].into(); // Vec<_> means "choose the Vec type for me"
                                             // Rust will choose Vec<i32>
}
```
#### [Proximo capítulo](https://github.com/justjapann/easy_rust_ptbr/blob/main/part1/tuples/tuples.md)