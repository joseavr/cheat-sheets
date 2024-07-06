# 🦀 Rust Ownership

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-05-04

---

# Intro to Ownership

What is Ownership?
- Data has single owner (who can manipulate this single data)
- Immutable aliases allowed
- Mutation only has 1 reference
- Ownership avoids double free
- Ownership replaces handles free() issues:

```rust
free(x)
```

## **Rules**:
1. Each `value` has one owner (`variable`)
2. Only one owner at a time
3. In terms of memory, when `owner` out of scope, the `value` is dropped (freed)

```rust
{
	let mut s = String::from("Hello"); // stored in heap
	s.push_str(" world"); // valid since s is mutable
	println!("{}", s); // compiles :)
}
```

- Since we only can have one owner, `x` losses ownership, `y` takes ownership
- If we were to print `x`, does not compile (rust yell us: it's unsafe!)
```rust
{
	let x = String::from("Hello"); // stored in heap
	let y = x; // hello was move from x to y
	
	println!("{}", y) // good
	println!("{}", x); // ERROR, y is owner, cannot print Hello
}
```
*Note: `y = s` is a shallow copy
Note: cannot take ownership back to `s` ( `s = y` ) unless we do another `let s = y`*

What happen here
```rust
let mut x = String::from("helllo")
// x is a mutable reference to the value hello
{
	let y = &mut x;
	// y is a mutable reference to the value hello
	// we cannot have more than one mutable reference so x becomes invalid for as long as  y exists
	pritnln!("{}", y, x);
} // y goes out of scope, so now x becomes valid again

x.push_str("world"); // we can use 'x'
println!("{}", x)
```


#### Example:
```rust
fn main() {
	let String::from("hello"); 
	{
		let b = a; // a is moved to b
		println!("b is {}",b);
	} // a is dropped, cannot longer be accessed outside scope
	println!("a is {}",a); // ERROR
}
```

```rust
fn main() {
	let a = 3; // stored in stack
	{
		let b = a; // a is moved to b
		println!("b is {}",b);
	} 
	println!("a is {}",a); // compiles fine
}
```

## Functions
- There are 3 ownership happening in this piece of code
```rust
{
  let s = String::from("Hello") // 1. s is owner
  let y = identity(s); // 3. x losses ownership, y is now the owner
  println!(y) // Fine
  println!(s) // Error
}

fn identity(x: String) -> String {
  x // pushed in the stack, s losses ownership, 2. x is now the owner
}
```


```rust
fn main() {
	let x = String::from("hello"); // x owns hello
	ley = funct(x);  // after funct is called, y is the owner of hello
	println!("{}", y);
}

fn funct(a:String) -> String {
	pritnln!("{}", a) // `a` still has ownership
	return a; // `a` is being passed back to the caller
} // returns 
```

How about dont want pass to pass owner -> `References`