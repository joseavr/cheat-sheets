# 🦀 Rust Borrowing

📚Class: CMSC330 Organization Programming

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/">Rust</a>

✏️Section: 0101

🗓️Date: 2023-05-02

---

# 🎬 Intro Borrowing
- **Declaring a variable to another variable's value (&)**
- Take a temporary reference to a variable or data structure values, without taking ownership of it
- When the borrower dies, the ownership gets back to the initial owner
```rust
{
	let x = String::from("Hello"); // owner: x->"Hello"
	let y = &x;  // borrower: y
}
```

Ex:
```rust
fn main() {
	let x = String::from("Hello");
	let y = get_len(x); // x (owner) itself is transferred directly to the gen_len(x)
	println!("{} is {} long", x, y)	
	
	fn get_len(x:String) -> u32 {
	  x.len()
	}
}
```

Ex:
```rust
fn main() {
	let x = String::from("Hello");
	let y = get_len(&x); // x's value is borrowed
	println!("{} is {} long", x, y)	
	
	fn get_len(x:&String) -> u32 {
	  x.len()
	}
}
```



## Deep Copy?
```rust
let y = identity( s.clone() )
```


# Rules of Borrowing/Reference

1. a) **Only one mutable** borrow/reference (pointer) at a time or 
1. b) **Any number of immutable** references (pointer) at any given time
2. All references must be valid. This means that the data being referenced must exist for at least as long as the reference.
3. **Cannot borrow** a variable as **mutable** and **immutable** at the same time.

Ex:
```rust
// fails because rule 1
let s  = String::from("Hello")
let s1 == &s; // 1.a
let s2 = &s; // 1.a

let s3 = &mut s; // 1.b -> fails
```

Ex: when borrowing, the variable being borrowed losses mutability, the new borrower also is immutable
```rust
{
	let mut x = String::from("Hello")
	 {
		 // x no longer mutable, losses mutability rules
		 let s2 = &x // s2 is also immutable
		 
		 println!("{} is {}", x, s2);
		 x.push.str("World") // fails, bc x not mutable anymore
		 s2.push.str("world") // fails, bc s2 not mutable
	 }
	x.push.str("world")
	// outscope of s2, x is mutable, can modify x
}
```

- Mutable -> Immutable
- **Cannot borrow something that is mutable**
```rust
let x = String::__
let y = &mut x; // fails, CANT mutate ref for immutable variables
// CAN mutate ref for mut variables
```

- We can do:
```rust
{
	let mut x = String::from("Hello")
	{
		let  y = &mut x; // borrows but dies in this scope
	}
	let z = &mut x; // CAN mutate ref for mut variables
	// Since there's no borrows, CAN borrow by rule 1
}
```

# Why these Rules Exists
- Prevents data races and use-after-free errors

## Data Race
- A data race occurs when two or more threads access the same piece of data at the same time, at least one of which is a write. 
- This can cause unpredictable behavior, data corruption, or crashes.
- Rust's ownership and borrowing rules prevent data races by ensuring that only one thread at a time can have mutable access to a piece of data.

## User-after-free Error
- A use-after-free error occurs when a program tries to use memory that has been deallocated. 
- This can happen if a program deallocates a piece of memory while other parts of the program are still using it. 
- Rust's **ownership** and **borrowing** rules prevent use-after-free errors by ensuring that memory is deallocated only when it is no longer being used.

Enforcing these rules at compile time, Rust can prevent these errors without requiring runtime checks or locks.

Allows Rust be memory safety and thread safety guarantees without sacrificing performance.

