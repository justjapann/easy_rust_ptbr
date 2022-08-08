## Alocação de memória

O stack, heap, e pointers são muito importantes em Rust.

O stack e o heap são dois lugarem que mantém a memória nos computadores. A diferença mais importante entre eles são:

- O stack é muito rápido, e o heap não tanto, também não é super lento, mas o stack sempre vai ser mais rápido. Porém, você não pode usar o stack a todo momento, por que:
- Rust precisa saber o tamanho da variável em tempo de compilação. Então variáveis simples como `i32` vão para a stack, por que sabemos exatamente seu tamanho. Você sempre vai saber que `i32` ocupa 4 bytes, por que 32 bits = 4 bytes. Então `i32` sempre pode ir para a stack.
- Mas alguns tipos nós não sabemos seu tamanho para tempo de compilação, e a stack precisa saber seu tamanho exato. Então como fazemos isso? Primeiro você coloca os dados na heap, por que a heap pode te dar o tamanho dos dados, e então para encontrá-lo o pointer vai para a stack, isso é bom por que sempre sabemos o tamanho do pointer. Então o computador primeiro vai para a stack, lê o pointer, e segue até o heap onde os dados estão.

Pointers parece complicado, mas eles são bem fáceis. Pointers se parecem com uma tabela em um livro. Imagine isso:

```text
MY BOOK
TABLE OF CONTENTS
Chapter                        Page
Chapter 1: My life              1
Chapter 2: My cat               15
Chapter 3: My job               23
Chapter 4: My family            30
Chapter 5: Future plans         43
```

Isso é como os cinco ponteiros, você pode ler eles e encontrar a informação que eles estão falando. Onde está "My life"? esta na página 1 (o _pointer_ na página 1). Onde está o cápitulo "My job?" Na página 23.

O pointer que você costuma ver em Rust se chama **reference**. Essa parte é muito importante você saber: uma referência aponta para uma memória de outro valor. Uma referência significa que você _aponta_ um valor, mas você não o tem. Isso é a mesma coisa do seu livro: a tabela de conteúdo não tem as informações, são os capítulos que as tem. Em Rust, referências tem o `&` na frente delas, então:

- `let my_variable = 8` cria uma variável comum, mas
- `let my_reference = &my_variable` cria sua referência.

Você lê `my_reference = &my_variable` como: "my_reference é uma referência para my_variable", ou: "my_reference se refere a my_variable".

Isso significa que `my_reference` esta apenas olhando os dados de `my_variable`. `my_variable` continua sendo o seu dado.

Você também pode ter referência de referências, ou qualquer número de referências.

```rust
fn main() {
    let my_number = 15; // isso é um i32
    let single_reference = &my_number; //  isso é um &i32
    let double_reference = &single_reference; // isso é um &&i32
    let five_references = &&&&&my_number; // isso é um &&&&&i32
}
```

Todos eles são de tipos diferentes, da mesma forma que "um amigo de um amigo" e diferente de "um amigo".

#### [Proximo capítulo](https://github.com/justjapann/easy_rust_ptbr/blob/main/part1/prints/prints.md)
