# 🦀 Rust Data Type

📚Class: CMSC 330 Organization of Programming Languages 

📓Subject: Rust

✏️Section: 0105 

🗓️Date: 2023-05-02

---

# 👨‍💻  Rust Data Types

**Type**:
- Scalar: flat types
- Integers: i64, i32, i16, i8, and isize = **sizeof(int)** (like in C)
- char: unicode char
- boolea: true, false
- float: f32,f64
- unsigned: u8, u16, u32, u64, usize

**Structure Types**:
- tuples: (t1, t2, t3, ...), and () // default value called unit
- strings: "Hello there"
- arrays: constant length (like in C)
	- [i32] // specific type
	- [i16,6] // type:i16, size:6
```rust

```

**3 Types of Loop**:
1. `loop { }`
2.  `while e { }`
3. `for pattern in e {}`
```rust
// 1. Loop
fn fact (n:u32) -> u32 {
  let mut a = n;  // `mut` mutable for the loop
  loop {
	  if a <= 1 { break ;}
	  a = a * n;
	  a = a + 1;
  }
  a // returns, no semicolon
}
```

```rust
// 2. While loop
fn fact(n: u32) -> u32 {
 let mut n = n;
 let mut a = 1;
 while a>1 {
	 a = a * n;
	 a = n - 1;
 }
 a
}
```

```rust
let num = [10;20;30]

for item in num.iter() {
	println!("The element is {}", item);
}
```

Rust has these but gonna behave differently
- struct -> C structs 
- enums -> Ocaml types
- traits -> Java interfaces

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