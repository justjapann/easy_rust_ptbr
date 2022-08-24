### Arrays

An array is data inside square brackets: `[]`. Arrays:

- must not change their size,
- must only contain the same type.

They are very fast, however.

The type of an array is: `[type; number]`. For example, the type of `["One", "Two"]` is `[&str; 2]`. This means that even these two arrays have different types:

```rust
fn main() {
    let array1 = ["One", "Two"]; // This one is type [&str; 2]
    let array2 = ["One", "Two", "Five"]; // But this one is type [&str; 3]. Different type!
}
```

Here is a good tip: to know the type of a variable, you can "ask" the compiler by giving it bad instructions. For example:

```rust
fn main() {
    let seasons = ["Spring", "Summer", "Autumn", "Winter"];
    let seasons2 = ["Spring", "Summer", "Fall", "Autumn", "Winter"];
    seasons.ddd(); // ⚠️
    seasons2.thd(); // ⚠️ as well
}
```

The compiler says, "What? There's no `.ddd()` method for seasons and no `.thd()` method for seasons 2 either!!" as you can see:

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

So it tells you `` method not found in `[&str; 4]` ``, which is the type.

If you want an array with all the same value, you can declare it like this:

```rust
fn main() {
    let my_array = ["a"; 10];
    println!("{:?}", my_array);
}
```

This prints `["a", "a", "a", "a", "a", "a", "a", "a", "a", "a"]`.

This method is used a lot to create buffers. For example, `let mut buffer = [0; 640]` creates an array of 640 zeroes. Then we can change zero to other numbers in order to add data.

You can index (get) entries in an array with []. The first entry is [0], the second is [1], and so on.

```rust
fn main() {
    let my_numbers = [0, 10, -20];
    println!("{}", my_numbers[1]); // prints 10
}
```

You can get a slice (a piece) of an array. First you need a &, because the compiler doesn't know the size. Then you can use `..` to show the range.

For example, let's use this array: `[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]`.

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

Remember that:

- Index numbers start at 0 (not 1)
- Index ranges are **exclusive** (they do not include the last number)

So `[0..2]` means the first index and the second index (0 and 1). Or you can call it the "zeroth and first" index. It doesn't have the third item, which is index 2.

You can also have an **inclusive** range, which means it includes the last number too. To do this, add `=` to write `..=` instead of `..`. So instead of `[0..2]` you can write `[0..=2]` if you want the first, second, and third item.
