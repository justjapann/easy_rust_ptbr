### Shadowing

**[Você pode ver esse capítulo no youtube](https://youtu.be/InULHyRGw7g)**

Shadowing significa usar `let` para declarar outra variável com o mesmo nome mas em outra variável. Isso se parece com mutabilidade, mas é completamente diferente. Shadowing se parece com:

```rust
fn main() {
    let my_number = 8; // Isso é um i32
    println!("{}", my_number); // printa 8
    let my_number = 9.2; // isso é um f64 com o mesmo nome. mas não é o primeiro my_number - ele é completamente diferente!
    println!("{}", my_number) // Printa 9.2
}
```

Aqui dizemos que "sombreamos" `my_number` com a nova declaração de let.

Então o primeiro `my_number` foi destruido? Não, mas quando nós chamamos `my_number` agora nós temos `my_number` com `f64`. Isso se da por estarem no mesmo escopo de bloco (o mesmo `{}`), por isso não podemos ver o primeiro `my_number` agora.

Mas se eles estiverem em diferentes blocos, podemos ver os dois. Por exemplo:

```rust
fn main() {
    let my_number = 8; // Isso é u, i32
    println!("{}", my_number); // printa 8
    {
        let my_number = 9.2; // isso é um f64. isso nao é o my_number - ele é completamente diferente!
        println!("{}", my_number) // Printa 9.2
                                  // mas esta escondendo que my_number vive somente aqui.
                                  // o primeiro my_number ainda continua vivo!
    }
    println!("{}", my_number); // printa 8
}
```

Então quando você sombrea uma variável, você não destroi ela. Você **bloqueia** ela.

Então, qual a vantagem de shadowing? Shadowing é bom quando você precisa trocar a variável muitas vezes. Imagine que você quer fazer muitas contas simples com a variável:

```rust
fn times_two(number: i32) -> i32 {
    number * 2
}
fn main() {
    let final_number = {
        let y = 10;
        let x = 9; // x começa com 9
        let x = times_two(x); // sombrea com o novo x: 18
        let x = x + y; // sombrea com o novo x: 28
        x // retorna x: final_number é o novo valor de x x
    };
    println!("The number is now: {}", final_number)
}
```

Sem o shadowing você teria que pensar em diferentes nomes, mesmo que você não se importe com x:

```rust
fn times_two(number: i32) -> i32 {
    number * 2
}
fn main() {
    // Exemplo de Rust sem shadowing
    let final_number = {
        let y = 10;
        let x = 9; // x comeca com 9
        let x_twice = times_two(x); // segundo nome para x
        let x_twice_and_y = x_twice + y; // terceiro nome de x!
        x_twice_and_y // muito ruim quando não temos shadowing - poderiamos apenas ter usado x
    };
    println!("The number is now: {}", final_number)
}
```

#### [Proximo capítulo](https://github.com/justjapann/easy_rust_ptbr/blob/main/part1/memory/memory.md)
