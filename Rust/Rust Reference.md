# Rust Reference

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-05-05

---

# Reference


#### Rule:
1. All references must be valid
2. Either but not obth of the follwoing must be true
	1. You can have as many immutable ref as you want OR (reader)
	2. You can have exactly 1 mutable ref (writer)
Only can only read or write, one at time
```rust
fn main() {
	let a = String::from("hello"); // allocated in heap
	let b = &a; // reference
	let c = b; // ownership
	println!("a is {}", a);
	println!("b is {}", b);
	println!("c is {}", c);
	println!("{} is {}", a,b);
}
```



```rust
fn main() {
	let mut a = String;:from("uello");
	{
		let b = &a; // b is immutable
		pritnk!("{}", b); // b lifetime (being used) ends here
		a.push_str(" World");
	} // b scope ends here
	println!("{}", a);

	// fine
}
```


```rust
fn main() {
	let mut a = String;:from("uello");
	{
		let b=  &mut a; // mutable ref
		pritnln!("{}", a);  // a mutable ref
		a.push_str(" World");
		pritnln!("{}", b); 
	} 
	// Does not compile, cant have 2 mut
}
```