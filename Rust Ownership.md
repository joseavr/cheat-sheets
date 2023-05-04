# Rust

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-05-04

---

# Intro 

- To avoid doing free(), owernship replaces this
```rust
free(x)
```

```rust
let mut x = String::from("helllo")
// x is a mutable reference to the value hello
{
	let y = &x;
	// y is a immutable reference to the value hello
	// we cannot have both a mutable reference ad a  immutable ref, so x is now immutable
	pritnln!("{}", y, x);
}

x. push_str("world");
println!("{}", x)
```

What happen here
```rust
```rust
let mut x = String::from("helllo")
// x is a mutable reference to the value hello
{
	let y = &mut x;
	// y is a mutable reference to the value hello
	// we cannot have more than one mutable reference so x becomes invalid for as long as  y exists
	pritnln!("{}", y, x);
} // y goes out of scope, so now x becomes valid again

x. push_str("world");
println!("{}", x)
```
```