# Rust Data Type

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-05-02

---

# Rust Data Types

Rust has these but gonna behave differently
- struct -> c structs 
- enums -> Ocaml types
- traits -> java interfaces

## Example
```rust
struct Rect {
	width: u32
	heigh: u32
}

impl Rect {
	fn area(&self) -> u32{
		self.width * self, height
	}

	fn newf(&sf, a:&u32) -> 
}

let r1 = Rect {width=5 ; height = 10; }
r1.area()
r1.newf(5)
```