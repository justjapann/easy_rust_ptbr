## Mutable references

**[Você pode ver esse capítulo no youtube](https://youtu.be/G48z6Rv76vc)**

Se você quer usar a referência para mudar os dados, você pode usar referências mutáveis. Para criar uma referência mutável, escreva `&mut` ao invés de `&`.

```rust
fn main() {
    let mut my_number = 8; // nao esqueca de escrever mut aqui!
    let num_ref = &mut my_number;
}
```

Então, quais os dois tipos? `my_number` é `i32`, e `num_ref` é `&mut i32` (nós dizemos "referência mutável a `i32`").

Vamos usar isso para adicionar 10 em my_number, porém você não pode escrever `num_ref += 10`, por que `num_ref` não é um `i32`, ele é um `&i32`. O valor está dentro do `i32`. Para chegar ao local onde o valor está, usamos `*`. `*` significa "Eu não quero a referência, eu quero o valor dela". Em outras palavras, um `*` é o oposto de `&`. Também, um `*` apaga um `&`.

```rust
fn main() {
    let mut my_number = 8;
    let num_ref = &mut my_number;
    *num_ref += 10; // Use * para mudar o valor do i32.
    println!("{}", my_number);
    let second_number = 800;
    let triple_reference = &&&second_number;
    println!("Second_number = triple_reference? {}", second_number == ***triple_reference);
}
```

Isso printa:

```text
18
Second_number = triple_reference? true
```

Porque usando `&` é chamado de "referencing", e usando `*` é chamado de "**de**referencing".

Rust tem duas regras para referências mutáveis e imutáveis. Elas são muito importantes, mas também fáceis de lembrar por fazerem sentido.

- **Regra 1**: Se você tiver apenas referências mutáveis, você pode ter quantas quiser: 1 é ok, 3 é ok, 1000 é ok, sem problemas.
- **Regra 2**: Se você tiver uma referência mutável, poderá ter apenas uma. Também, você não pode ter uma referência imutável **e** uma referência mutável juntas.

Isso é por que referências mutáveis podem mudar os valores. Você pode ter problemas se alterar dados quando referências estiverem lendo eles.

Uma boa maneira de entender é pensar em uma apresentação de Powerpoint.

Situação um sobre **apenas referência mutável**.

Situação um: Um funcionário está escrevendo um apresentação Powerpoint, ele quer que o seu gerente o ajude, então ele deu suas informações de login ao gerente, e pede para ele ajudar nas edições. Agora o gerente tem uma referência mutável da apresentação do funcionário. O gerente pode fazer quantas mudanças ele quiser, e devolver o computador mais tarde. Isso é ok, por que ninguém vai estar vendo a apresentação.

Situação dois sobre **apenas referência imutável**.

Situação dois: O funcionário está dando uma apresentação a 100 pessoas. Todas as 100 pessoas podem ver os dados do funcionário,Eles tem todas referências imutáveis da apresentação do funcionário. Isso é ok, por que ninguém pode mudar os dados.

Situação três sobre **o problema da situação**.

Situação três: O funcionário da ao gerente as informações de login, o gerente agora tem as referências mutáveis. Em seguida, o funcionário está dando a apresentação para 100 pessoas, mas o gerente continua logado. Isso não é bom, por que o gerente pode fazer qualquer coisa que quiser. Talvez o gerente pode estar logado e enviar um email a sua mãe! Agora as 100 podem ver o gerente escrevendo o email para sua mãe em vez da apresentação. Isso não é oque eles esperavam ver.

aqui está uma referência mutável e imutável:

```rust
fn main() {
    let mut number = 10;
    let number_ref = &number;
    let number_change = &mut number;
    *number_change += 10;
    println!("{}", number_ref); // ⚠️
}
```

O compilador printa uma mensagem de ajuda para mostrar seu problema.

```text
error[E0502]: cannot borrow `number` as mutable because it is also borrowed as immutable
 --> src\main.rs:4:25
  |
3 |     let number_ref = &number;
  |                      ------- immutable borrow occurs here
4 |     let number_change = &mut number;
  |                         ^^^^^^^^^^^ mutable borrow occurs here
5 |     *number_change += 10;
6 |     println!("{}", number_ref);
  |                    ---------- immutable borrow later used here
```

De qualquer jeito, o código vai funcionar. Por que?

```rust
fn main() {
    let mut number = 10;
    let number_change = &mut number; // cria uma referência mutável
    *number_change += 10; // usa a referencia para adicionar 10
    let number_ref = &number; // cria uma referencia imutavel
    println!("{}", number_ref); // printa a referencia imutavel
}
```

Isso printa `20` sem problemas. Vai funcionar por que o compilador é inteligente o suficiente para entender seu código. Ele sabe que você está usando `number_change` para trocar `number`, mas não ta usando ele denovo, então aqui não tem problema. Nós não estamos usando uma referência mutável e imutável juntas.

Inicialemnte em Rust esse tipo de código gerava erro, mas o compilador é inteligente agora. Ele pode entender não apenas oque so digitamos, mas como usar aquilo também.

#### [Proximo capítulo](https://github.com/justjapann/easy_rust_ptbr/blob/main/part1/shadowing/shadowing_again.md)
