# Rust Reference

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-05-05

---

# Reference

We need to use the `*` symbol to access the value of the reference, which is an `i32`, and compare it with `s` and `e`.

Here is an example to demonstrate when to use the `*` symbol in Rust:
```rust
fn main() {
    let x = 10;
    let y = &x; // y is a reference to x
    
    println!("The value of x is {}", x); // prints "The value of x is 10"
    println!("The value of y is {}", y); // prints "The value of y is 10" (dereferencing happens implicitly here)
    println!("The value of *y is {}", *y); // prints "The value of *y is 10" (dereferencing explicitly using * operator)
}

```

In this example, `y` is a reference to `x`. When we print `y` without using the `*` symbol, Rust implicitly dereferences the reference and prints the value of `x`. When we print `*y`, we explicitly dereference the reference using the `*` symbol, which gives us the value of `x`. We use the `*` symbol to access the value that `y` points to.

-