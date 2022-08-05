### Primitive types

**[Você pode ver esse capítulo no youtube](https://youtu.be/OxTPU5UGMhs)**

Rust tem tipos simples chamados de **primitive types**(primitive = muito simples). Nós vamos começar com os inteiros e os `char` (caracteres). Inteiros são números que não tem números decimais. Existem dois tipos de inteiros:

- Inteiros com sinal,
- Inteiros sem sinal.

Com sinal `+` (sinal de adição) e `-` (sinal de redução), inteiros com sinal podem ser positivos ou negativos (e.g. +8, -8). Mas inteiros sem sinal podem ser somente positivos, por eles não terem um sinal.

Os inteiros com sinal são: `i8`, `i16`, `i32`, `i64`, `i128`, e `isize`.
Os inteiros sem sinal são: `u8`, `u16`, `u32`, `u64`, `u128`, e `usize`.

O número depois do i ou u signifíca a quantidade de bits para o número, então números com mais bits podem ser maiores. 8 bits = 1 byte, assim `i8` equivale a 1 byte, `i64` a 8 bytes, e assim por diante. Tipos numéricos com um grande valor podem segurar grandes números. Por exemplo, um `u8` pode segurar até 255, mas o `u16` pode segurar até 340282366920938463463374607431768211455.

Então oque é `isize` e `usize`? Eles significam o número de bits de cada computador (o número de bits do seu computador se chama **arquitetura** do computador). Então `isize` e `usize` em computadores de 64-bit são como `i64` e `u64`.

Existem muitas razões para diferentes tipos de inteiros. A primeira razão é a performace do computador: um pequeno número de bytes tem um rápido processo. Por exemplo, o número -10 como um `i8` é `11110110`, mas como um `i128` é um `11111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111110110`. Aqui estão mais alguns outros usos:

Caracteres em Rust são chamados de `char`. Todo `char` tem um número: a letra `A` é o número 65, enquanto o caracteres `友` ("amigo" em Chines) é o número 21451. A lista de números é chamada de "Unicode". Unicode usa números menores para caracteres que são mais usados, como A até Z, ou os dígitos de 0 até 9, ou espaço.

```rust
fn main() {
    let first_letter = 'A';
    let space = ' '; // Um espaço dentro de ' ' também é um char
    let other_language_char = 'Ꮔ';
    let cat_face = '😺'; // Emojis são chars também
}
```

Aqui está a razão:

```text
error[E0604]: only `u8` can be cast as `char`, not `i32`
 --> src\main.rs:3:20
  |
3 |     println!("{}", my_number as char);
  |                    ^^^^^^^^^^^^^^^^^
```

Felizmente nós podemos corrigir isso com `as`. Nós não podemos converter `i32` a um `char`, mas podemos converter um `i32` a `u8`, e então podemos fazer o mesmo com `u8` para `char`. Em uma linha nós usamos `as` para criar my_number em `u8`, e denovo para torná-lo um `char`. Agora isso vai compilar:

```rust
fn main() {
    let my_number = 100;
    println!("{}", my_number as u8 as char);
}
```

Isso printa um `d` porque esse é o `char` de lugar 100.

A maneira mais fácil de qualquer jeito é apenas dizer a Rust que `my_number` é um `u8`. Você pode fazer isso assim:

```rust
fn main() {
    let my_number: u8 = 100; //  troque my_number para my_number: u8
    println!("{}", my_number as char);
}
```

Portanto, essas são as duas razões para ter tantos tipos de números diferentes em Rust. Aqui está outra razão: `usize` é o tamanho que Rust usa para _indexar_. (indexar significa "qual item vem primeiro", "qual item vem segundo", etc.) `usize` é a melhor maneira para indexar algo por causa de:

- O index não pode ser negativo, então ele precisa ser um numero com u.
- Ele deve ser grande, por que as vezes você precisa indexar muitas coisas, mas...
- Ele não pode ser um u64 por causa que computadores 32-bit não usam u64.

Então Rust usa `usize` para que seu computador possa pegar o maior número indexado e poder o ler.

Vamos começar a aprender mais sobre `char`. Você pode dizer que `char` sempre vai ser um caracter, e usar `''` ao invés de `""`.

Todos `chars` usam 4 bytes da memória, desde que 4 bytes seja suficiente para segurar o tipo do caracter:

- Letras básicas e símbolos vão precisar de 1 de 4 bytes: `a b 1 2 + - = $ @`
- Outras letras, como tremas ou acentos alemães precisam de 2 de 4 bytes: `ä ö ü ß è é à ñ`
- Caracteres Coreanos, Japoneses e Chineses precisam de 3 de 4 bytes: `国 안 녕`

Quando você usar caracteres como parte de uma string, a string vai ser codificada para usar a menor quantidade de memória necessária para cada caracter.

Nós podemos usar `.len()` para ver sobre isso:

```rust
fn main() {
    println!("Size of a char: {}", std::mem::size_of::<char>()); // 4 bytes
    println!("Size of string containing 'a': {}", "a".len()); // .len() te da o tamanho da string em bytes
    println!("Size of string containing 'ß': {}", "ß".len());
    println!("Size of string containing '国': {}", "国".len());
    println!("Size of string containing '𓅱': {}", "𓅱".len());
}
```

Isso printa:

```text
Size of a char: 4
Size of string containing 'a': 1
Size of string containing 'ß': 2
Size of string containing '国': 3
Size of string containing '𓅱': 4
```

Você pode ver que `a` é um byte, o alemão `ß` é dois, o kanji `国` é três, e a letra egípcia `𓅱` são 4 bytes.

```rust
fn main() {
    let slice = "Hello!";
    println!("Slice is {} bytes.", slice.len());
    let slice2 = "안녕!"; // "oi" em coreano
    println!("Slice2 is {} bytes.", slice2.len());
}
```

Isso printa:

```text
Slice is 6 bytes.
Slice2 is 7 bytes.
```

`slice` é 6 caracteres de tamanho e 6 bytes, mas `slice2` é 3 caracteres e seu tamanho é de 7 bytes.

Se `.len()` te da o tamanho em bytes, e o tamanho em caracteres? Nós vamos aprender sobre isso mais tarde, mas você pode relembrar que `.chars().count()` nós da isso. `.chars().count()` transforma oque você escreveu em caracteres e conta quantos são.

```rust
fn main() {
    let slice = "Hello!";
    println!("Slice is {} bytes and also {} characters.", slice.len(), slice.chars().count());
    let slice2 = "안녕!";
    println!("Slice2 is {} bytes but only {} characters.", slice2.len(), slice2.chars().count());
}
```

Isso printa:

```text
Slice is 6 bytes and also 6 characters.
Slice2 is 7 bytes but only 3 characters.
```
