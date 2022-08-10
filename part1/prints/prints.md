## Mais sobre prints

Em Rust você pode printar tudo que você quiser. Aqui esta mais algumas coisas que você precisa saber sobre prints.

Adicionando `\n` nós temos uma nova linha, e `\t` nós temos um novo espaço:

```rust
fn main() {
    // Note: isso é um print!, não um println!
    print!("\t Start with a tab\nand move to a new line");
}
```

Isso printa:

```text
         Start with a tab
and move to a new line
```

Dentro de `""` você pode escrever muitas linhas sem problemas, mas cuidado com os espaçamentos:

```rust
fn main() {
    // Nota: depois da primeira linha, voce tem que comecar na extrema esquerda.
    // Se você escrever diretamente em println!, ele vai adicionar os espaços
    println!("Inside quotes
you can write over
many lines
and it will print just fine.");
    println!("If you forget to write
    on the left side, the spaces
    will be added when you print.");
}
```

Isso printa:

```text
Inside quotes
you can write over
many lines
and it will print just fine.
If you forget to write
    on the left side, the spaces
    will be added when you print.
```

Se você quer printar os caracteres como `\n` (chama-se "escape characters"), você pode so adicionar um `\` extra:

```rust
fn main() {
    println!("Here are two escape characters: \\n and \\t");
}
```

Isso printa:

```text
Here are two escape characters: \n and \t
```

As vezes você pode ter muitos `"` e escape characters, e quer que Rust ignore tudo. Para isso, você pode adicionar `r#` no começo e `#` no final.

```rust
fn main() {
    println!("He said, \"You can find the file at c:\\files\\my_documents\\file.txt.\" Then I found the file."); // We used \ five times here
    println!(r#"He said, "You can find the file at c:\files\my_documents\file.txt." Then I found the file."#)
}
```

Isso printa a mesma coisa, mas usando `r#` fica mais fácil para as pessoas lerem.

```text
He said, "You can find the file at c:\files\my_documents\file.txt." Then I found the file.
He said, "You can find the file at c:\files\my_documents\file.txt." Then I found the file.
```

Se você precisa printar algo com `#` dentro, então você pode começar com `r##` e terminar com `##`. E se você precisa de mais uma, adicione mais um # do lado.

Aqui estão alguns exemplos:

```rust
fn main() {
    let my_string = "'Ice to see you,' he said."; // single quotes
    let quote_string = r#""Ice to see you," he said."#; // double quotes
    let hashtag_string = r##"The hashtag #IceToSeeYou had become very popular."##; // Has one # so we need at least ##
    let many_hashtags = r####""You don't have to type ### to use a hashtag. You can just use #.""####; // Has three ### so we need at least ####
    println!("{}\n{}\n{}\n{}\n", my_string, quote_string, hashtag_string, many_hashtags);
}
```

Isso vai printar:

```text
'Ice to see you,' he said.
"Ice to see you," he said.
The hashtag #IceToSeeYou had become very popular.
"You don't have to type ### to use a hashtag. You can just use #."
```

`r#` tem outro uso: você consegue usar junto de uma palavra chave (`let`, `fn`, etc.) como nome de variáveis.

```rust
fn main() {
    let r#let = 6; // o nome da variavel é let
    let mut r#mut = 10; // o nome da variavel é mut
}
```

`r#` tem essa função por que nas versões antigas do Rust tinham menos palavras chaves do que atualmente. Então com `r#` você pode evitar erros com nomes de variáveis que não eram palavras chaves antes.

Ou talvez por algum motivo você _realmente_ precisa de uma função com o nome `return`. Você pode escrever assim:

```rust
fn r#return() -> u8 {
    println!("Here is your number.");
    8
}
fn main() {
    let my_number = r#return();
    println!("{}", my_number);
}
```

Isso printa:

```text
Here is your number.
8
```

Você provavelmente não vai precisar disso, mas se você realmente tiver necessidade, use `r#` para definir as palavras chave.

Se você quer printar os bytes de um `&str` ou `char`, você so precisar escrever `b` antes da string. Isso funciona com todos ASCII caracteres. Esses são todos os ASCII caracteres:

```text
☺☻♥♦♣♠♫☼►◄↕‼¶§▬↨↑↓→∟↔▲▼123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~
```

Então, para imprimir isso:

```rust
fn main() {
    println!("{:?}", b"This will look like numbers");
}
```

Here is the result:

```text
[84, 104, 105, 115, 32, 119, 105, 108, 108, 32, 108, 111, 111, 107, 32, 108, 105, 107, 101, 32, 110, 117, 109, 98, 101, 114, 115]
```

Para `char` isso é chamado de _byte_, e para `&str` _byte string_.

Você também pode colocar `b` e `r` juntos se precisar:

```rust
fn main() {
    println!("{:?}", br##"I like to write "#"."##);
}
```

Isso vai printar `[73, 32, 108, 105, 107, 101, 32, 116, 111, 32, 119, 114, 105, 116, 101, 32, 34, 35, 34, 46]`.

Também tem um Unicode escape que permite printar qualquer caracter Unicode dentro de uma string: `\u{}`. O número hexadecimal vai para dentro do `{}` e printa ele. Esse é um pequeno exemplo de como pegar um número Unicode, e como printar ele na sequência.

```rust
fn main() {
    println!("{:X}", '행' as u32);
    println!("{:X}", 'H' as u32);
    println!("{:X}", '居' as u32);
    println!("{:X}", 'い' as u32);
    println!("\u{D589}, \u{48}, \u{5C45}, \u{3044}"); // tenta printar ele com um unicode escape \u
}
```

Nós sabemos que `println!` pode printar com `{}` (para Display) e `{:?}` (para Debug), mais `{:#?}` para um print bonito. Mas existem outras maneira de printar.

Por exemplo, se você tem uma referência, você pode usar `{:p}` para printar o _pointer address_. Pointer address significa a localização na memória do seu computador.

```rust
fn main() {
    let number = 9;
    let number_ref = &number;
    println!("{:p}", number_ref);
}
```

Isso printa `0xe2bc0ffcfc` ou algum outro endereço, pode ser diferente cada vez, dependendo de onde seu computador o armazena.

Ou você pode printar um binary, hexadecimal e octal:

```rust
fn main() {
    let number = 555;
    println!("Binary: {:b}, hexadecimal: {:x}, octal: {:o}", number, number, number);
}
```

Isso printa `Binary: 1000101011, hexadecimal: 22b, octal: 1053`.

Você também pode adicionar números para alterar a order, a primeira variável tem o index 0, o próximo tem index 1, e assim por diante.

```rust
fn main() {
    let father_name = "Vlad";
    let son_name = "Adrian Fahrenheit";
    let family_name = "Țepeș";
    println!("This is {1} {2}, son of {0} {2}.", father_name, son_name, family_name);
}
```

`father_name` está na posição 0, `son_name` está na posição 1, e `family_name` está na posição 2. Então isso vai printar `This is Adrian Fahrenheit Țepeș, son of Vlad Țepeș`.

Talvez você tem uma string muito complexa com várias variáveis dentro do `{}`, ou talvez você precisa printar a variável mais de uma vez, você pode usar mais de um `{}` para isso:

```rust
fn main() {
    println!(
        "{city1} is in {country} and {city2} is also in {country},
but {city3} is not in {country}.",
        city1 = "Seoul",
        city2 = "Busan",
        city3 = "Tokyo",
        country = "Korea"
    );
}
```

Isso vai printar:

```text
Seoul is in Korea and Busan is also in Korea,
but Tokyo is not in Korea.
```

Prints muito complexos também são possíveis em Rust se você precisar deles. Aqui está como fazer isso:

1. Você quer um nome de uma variável? Escreva ela primeiro, como quando a gente fez {country} acima.
   (Então adicione `:` depois disso se você quer adicionar mais coisas)
2. Você quer um caracter de preenchimento? Por exemplo, 55 com três "padding zeros" se parece com 00055.
3. Qual alinhamento (left / middle / right) para o espaçamento?
4. Você quer o tamanho mínimo? (apenas escreva o número number)
5. Você quer o tamanho máximo? (escreve o número com o `.` na frente)

Por exemplo, se você quer escrever "a" com cinco ㅎ caracteres na esquerda e cinco ㅎ caracteres na direita:

```rust
fn main() {
    let letter = "a";
    println!("{:ㅎ^11}", letter);
}
```

Isso printa `ㅎㅎㅎㅎㅎaㅎㅎㅎㅎㅎ`. vejamos 1) a 5) para entender isso, como o compilador vai ler.

- Você quer um nome de uma variável? `{:ㅎ^11}` Não tem nome de variável, não tem nada antes de `:`.
- Você quer um caracter de preenchimento? `{:ㅎ^11}` Sim. ㅎ vem depois de `:` e tem um `^`. `<` significa preenchimento com o caractere à esquerda, `>` significa à direita, e `^` significa no centro.
- Você quer o tamanho mínimo? `{:ㅎ^11}` Sim: tem um 11 depois.
- Você quer o tamanho máximo? `{:ㅎ^11}` Não: não tem nenhum número com `.` antes.

Aqui está alguns exemplos de tipos de formatação.

```rust
fn main() {
    let title = "TODAY'S NEWS";
    println!("{:-^30}", title); // sem nome de variavel, tem -, coloque no centro, 30 caracteres de tamanho
    let bar = "|";
    println!("{: <15}{: >15}", bar, bar); // sem nome de variavel, espaco, 15 caracteres cada, um na esquerda, one na direita
    let a = "SEOUL";
    let b = "TOKYO";
    println!("{city1:-<15}{city2:->15}", city1 = a, city2 = b); // nome de variavel city1 e city2, -, um na esquerda, one na direita
}
```

Isso printa:

```text
---------TODAY'S NEWS---------
|                            |
SEOUL--------------------TOKYO
```

#### [Proximo capítulo](https://github.com/justjapann/easy_rust_ptbr/blob/main/part1/strings/strings.md)
