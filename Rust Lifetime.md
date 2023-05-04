# Rust Lifetime

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-05-04

---

# Lifetime
- Lifetime is not the same as a block code
- **Lifetime is from variable is initialized and when it last called/used**
- Main point is to get rid of dangling pointers
```rust
{
	let mut s = String::from("Hello")
	let r1 = &s;
	let r2 = &s;
	println!("{} = {}", r1, r2); // r1, r2 are no longer used (lifetime ends here)
	
	let r3 = &mut s; // 
	println!("{}", r3);
	println! ("{}", r1); // fails
}
``` 


- Find the issue here? Dangling pointer, memory issues
```rust
fn main {
	let ref = d();
	pritnln! ("{}", ref)
}

fn d() -> &string{
	let s = String::from("Hello");  // s->Hello
	&s
}
```
- **Lifetime of owner >= lifetime of the ref to owner**

- What is the lifetime of this?
```rust
{
	let r;
	{
		let s = String::from("Hello")
		r = &s; // s liftetime
	}

	println!("{}", r); // r lifetime
	
}

// However, s >= r lifetime
// So this program fails
```


- Another Lifetime example
- What is the issue?
```rust
fn main() {
	let x = String::from("Hello")
	{
		let y = String::from("bye") // y owner of value bye
		let res = longest(&s, &y);
		prontln!("{} is longer", res)
	}
}

// Consider
fn longest9a:&String, b:&String) -> &String{
	if a.len > b.len {a} else {b}
}
```

```rust
fn longest<'a>(a:&'a string, b:&'a string) -> &'a string {
	// a and b needs to life at least as long as the return
}
```

- Rust treats lifetime as extension of type
```rust
3:int
4.0:float

x:isize for the lifetime of 'a
y:f32 for the liftime of 'b

// how about in a func def
fn foo(a:&int) -> &int {

}

1) rust will add a different lfietime to all input parameters that are a reference
2) if one lifetime parameter, then output has the same
3) if multiple inputs AND one is self or &self, then lifetime of ouput is same as self or &self

let f x = x+1; //ocaml does type inference

//rust does lifetime inference
fn foo(a:&'a int) -> &'a int {

}

// rule 1, rule 2 no apply, rule 3 no apply
fn bar(x:&a' u32, y: &'b u32) -> &'? u32 {
	// explicit lifetime parameters do not change the actual lifetime of anything
	// all it does is help the rust compiler to know when it should expect tings to live
}


fn bar(x:&a' u32, y: &'b u32) -> &'a u32 {

}

- We want to avoid dangling pointers
lifetime of return value is at maximum the lifetime of the input its linked to
```

## Rust Lifetime Rules

1. Compiler will assign a different lifetime parameter. Each parameter is a reference
```rust
fn foo(a:&'a is 32, b:&'b u32) // rust adds this
fn foo( a: &; 32, b;& u32); // programmer
```

2. if there is a exactly one lifetime parameter that lifetime is assigned to all ouput references
```rust
fn bar(a:&i32) -> &i32 // programmer
fn bar(a;&'ai32) -> &'ai32 // rust adds this
```

3. If there is multiple input parameters **and** one of the references is sekf ir &self **then** the output lifetime becomes the same as self or &self. (& = reference, &self = this in objects)
Example: 
- First second, third, rule does not apply
- Rust does not know what to do here and yells
- Make explicit
```rust
fn longest (a;&'a string, b&'b string') -> & string
```


