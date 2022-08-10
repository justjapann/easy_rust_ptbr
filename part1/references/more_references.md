## More on references

**[See this chapter on YouTube](https://youtu.be/R13sQ8SNoEQ)**

References are very important in Rust. Rust uses references to make sure that all memory access is safe. We know that we use `&` to create a reference:

```rust
fn main() {
    let country = String::from("Austria");
    let ref_one = &country;
    let ref_two = &country;
    println!("{}", ref_one);
}
```

This prints `Austria`.

In the code, `country` is a `String`. We then created two references to `country`. They have the type `&String`, which you say is a "reference to a String". We could create three references or one hundred references to `country` and it would be no problem.

But this is a problem:

```rust
fn return_str() -> &str {
    let country = String::from("Austria");
    let country_ref = &country;
    country_ref // ⚠️
}
fn main() {
    let country = return_str();
}
```

The function `return_str()` creates a String, then it creates a reference to the String. Then it tries to return the reference. But the String `country` only lives inside the function, and then it dies. Once a variable is gone, the computer will clean up the memory and use it for something else. So after the function is over, `country_ref` is referring to memory that is already gone, and that's not okay. Rust prevents us from making a mistake with memory here.

This is the important part about the "owned" type that we talked about above. Because you own a `String`, you can pass it around. But a `&String` will die if its `String` dies, so you don't pass around "ownership" with it.
