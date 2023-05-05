# Rust Lifetime

📚Class: CMSC 330 Organization of Programming Languages 

📓Subject: Rust 

✏️Section: 0105 

🗓️Date: 2023-05-04

---

# ⏳ Lifetime
- Lifetime is not the same as a block code
- **Lifetime of a variable is from when initialized to when it last called/used**
- Main point is to get rid of dangling pointers
```rust
{
	let mut s = String::from("Hello")
	let r1 = &s; // r1's lifetime starts here 
	let r2 = &s; // r2's lifetime starts here
	println!("{} = {}", r1, r2); // r1, r2 are no longer used (lifetime ends here)
	
	let r3 = &mut s; // r1, r2 dropped, can make r3 mut allowed
	println!("{}", r3); // good
	// if we add this, fails bc 1 mut AND multiple immut refs
	println! ("{}", r1); 
}
``` 


- Find the issue here? Dangling pointer, memory issues
- After func call, s gets dropped, &s will become a **dangling pointer**
- **Lifetime of owner >= lifetime of the ref to owner then FAILS**
```rust
fn main {
	let ref = d();
	// s !>= &s -> FAILS
	pritnln! ("{}", ref) // Fails, s does no live long enough
}

fn d() -> &String{
	let s = String::from("Hello");  // s->Hello
	&s // Without `&`, no issue
} // s dealocated, but &s still being used by `return`
```
*Note: Dangling Pointer is when trying to use a pointer outside of scope*

- What is the lifetime of this?
```rust
{
	let r;
	{
		let s = String::from("Hello");
		r = &s; // s liftetime
	} // s out of scope and dealocatted, but &s being used by r

	println!("{}", r); // fails, s does not live long enough
	// s !>= &s
}
// FAILS
```


## Generic Lifetimes (Properly Returning values from Function)

- What is the issue?
- Lifetime of the returned reference is not specified, so it defaults to the shorter of the lifetimes of the input references.
- Since `a` and `b` are local variables, their lifetime ends at the end of their respective scopes in the if statement.
- Therefore, a and b must live as long as the lifetime of `y`. However, this is not the case causing FAIL
```rust
fn main() {
	let x = String::from("Hello")
	{
		let y = String::from("bye")
		let res = longest(&x, &y);
		println!("{} is longer", res)
	}
} // FAILS

// Consider
fn longest (a: &String, b: &String) -> &String{
	if a.len() > b.len() {a} else {b}
	// a and b needs to live at least as long as the return
} 
```

- To fix, specify the lifetime of the returned reference to be the same as longer of the lifetimes of the input references
```rust
// PASSES
fn longest<'a>(a: &'a String, b: &'a String) -> &'a String{
	if a.len() > b.len() {a} else {b}
	// a and b live as long as the return
} // Passes
```


## Lifetime Rules

1. Compiler will assign a different lifetime to each input parameters that is a reference
```rust
fn foo(a: &i32, b: &u32); // programmer
fn foo(a: &'a i32, b: &'b u32) // rust adds this
```

2. if there is a exactly one lifetime parameter, that lifetime is assigned to all ouput references
```rust
fn bar(a: &i32) -> &i32 // programmer
fn bar(a: &'a i32) -> &'ai32 // rust adds this
```

3. If there is multiple input parameters **AND** one of the references is self/&self **THEN** the output lifetime becomes the same as &self (&self = 'this' in objects)

Example: 
- Only first rule applies
- Rust does not know what to do here and yells bc `-> & String`
- Make explicit:  `-> &a' String` OR `-> &b' String`
```rust
fn longest (a: &'a String, b: &'b String') -> & String
```

### Example
```rust
// rule 1 applies , rule 2 and 3 no apply
fn bar(x:&a' u32, y: &'b u32) -> &'? u32 {
	// explicit lifetime parameters do not change the actual lifetime of anything
	// all it does is help the rust compiler to know when it should expect tings to live
}
```

### OCAML vs RUST
```rust
let f x = x+1; //ocaml does type inference

fn foo(a:&'a int) -> &'a int { } //rust does lifetime inference
```