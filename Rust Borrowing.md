# Rust Borrowing

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-05-02

---

# Intro Borrowing

## Rules of Borrowing

1. a) One mutable reference (pointer) at a time
1. b) Only number of immutalble reference (pointer) at a time
2. a) All references must be valid
2. b) 

```rust
{
	let mut x = String::from("Hello")
	 {
		 let s2 = &x // x no longer mutable access, losses mutability rules
		 // s2 is now mutable
		 println!("{} is {}", x, s2);
		 x.push.str("World") // fails
		 s2.push.str("world") // fails
	 }
	x.push.str("world") // outscope, mutability back, can use push
}
```
- Mutable -> Immutable
- Cannot borrow something that is mutable
```rust
let y = &mut x; // fails
```

- We can do:
```rust
{
	let mut x = String::from("Hello")
	{
		let  y = &mut x;
	}
	let z = &mut x; // works fine
}
```

## Why these Rules Exists
- Prevents data base'


