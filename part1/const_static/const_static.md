## const e static

**[Você pode ver esse capítulo no youtube](https://youtu.be/Ky3HqkWUcI0)**

Existem duas outras formas de declarar valores, e não apenas com `let`. Eles são `const` e `static`. Também, Rust não vai usar inferência de tipos: você precisa escrever o tipo para ele. Eles são valores que não podem ser mudados (`const` significa constante). A diferença entre eles é:

- `const` é para valores que não podem ser mudados, o nome é substituido pelo valor quando usado,
- `static` é similar a `const`, mas ele não tem uma memória de locação física e pode ser uma variável global.

Então eles são quase iguais. Programadores Rust sempre usam `const`.

Você pode escrever o nome com TODAS AS LETRAS MAIUSCÚLAS, e normalmente fora da `main` para que possa ser usado em todo o programa.

Dois exemplos são: `const NUMBER_OF_MONTHS: u32 = 12;` e `static SEASONS: [&str; 4] = ["Spring", "Summer", "Fall", "Winter"];`
