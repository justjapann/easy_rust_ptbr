### Variáveis sem valores

Uma variável sem valor é chamada de "variável inutilizada". Unitilizada significa "ela ainda não começou". Elas são simples: apenas escreva `let` e o nome da variável:

```rust
fn main() {
    let my_variable; // ⚠️
}
```

Mas você não pode usá-lo ainda, e o Rust não compilará se algo não for inicializado.

As vezes elas podem ser muito úteis, aqui está um exemplo disso:

- Você tem um código de bloco e um valor de variável dentro dele, e
- A variável precisa viver fora do bloco de código.

```rust
fn loop_then_return(mut counter: i32) -> i32 {
    loop {
        counter += 1;
        if counter % 50 == 0 {
            break;
        }
    }
    counter
}
fn main() {
    let my_number;
    {
        // Pretend we need to have this code block
        let number = {
            // Pretend there is code here to make a number
            // Lots of code, and finally:
            57
        };
        my_number = loop_then_return(number);
    }
    println!("{}", my_number);
}
```

Isso printa `100`.

Você pode ver que `my_number` foi declarado na função `main()`, então ele continua vivo até o fim, mas pega seu valor de dentro do loop. De qualquer jeito, esse valor vive em `my_number`, por que `my_number` tem o valor. E se você escreveu `let my_number = loop_then_return(number)` dentro do bloco, ele vai morrer imediatamente.

Fica mais fácil de imaginar se você simplificar o código. `loop_then_return(number)` dá o resultado 100, então vamos deleter e escrever `100` em vez dele. Também, agora não precisamos de `number`, então vamos deletar ele também. Vai ficar parecido com isso:

```rust
fn main() {
    let my_number;
    {
        my_number = 100;
    }
    println!("{}", my_number);
}
```

Isso é quase o mesmo de `let my_number = { 100 };`.

Note também que `my_number` não é `mut`, ele não recebeu um valor até obter 100, então ele nunca mudou seu valor. No final, o real código de `my_number` é apenas `let my_number = 100;`.

#### [Proximo capítulo](https://github.com/justjapann/easy_rust_ptbr/blob/main/part1/types/collection_types.md)
