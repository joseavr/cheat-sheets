# 🦀 Rust

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-11-14

---

# Intro Rust

- Created by Mozilla 
- First comipler written in Ocaml, then in built in Rust
- Replaces C
- Low level Language
- Famous for creating blazingly fast Compilers (e.g Next.js)
- Works well with low level

```rust
// hello.rs
fn main() {
	println!("Hello, world!");
}
```

- Compiler language with rustc commmand
```bash
rustc hello.rs
```

#### Semicolon `;`
- If `;` tells rust this is a statement
- If no `;` tells rust this line is an expression
	- In functions, the line with no `;` is returned
- Replaces the keyword`return`
- Since we using u32, we can control memory efficiently with rust
- Expressions does not need semicolons (e.g `pritnln!()`)
```rust
fn other3(x: u32) ->u32{ // u32: unsigned 32 bits
  let res = x + 1;
  println!("u32 ({}) -> u32({})", x.res);
  res // this returns
}
```

#### Codeblocks: `{}`
- /statement;* expr?}/
- Codeblocks are expressions 
- A function is a codeblock (where returns one expression or nothing)
- Default return type of  an empty codeblock is `unit` (no expressions in `{})
- Unit is the size of the machine size: 4 bytes, 8 bytes, deoending on the machine
- No more than one expression in a codeblock

```rust
{
  let x =3;
  let y = 4;
  x+y
} : usize(7)
```

```rust
{
  let x =3;
  let y = 4;
  x+y;
} : unit
```


#### if statement
- Rust needs and else block like in Ocaml

```rust
let x = (if x ==5 {
	6;
})
```

```rust
// compiles fine
let x = if true { false} else {true};
pritnln!("{}". x)
```

```rust
// compiler yells
let x = if  false {false};
pritnln!("{}". x)
```

```rust
// compiles
if  false {false;};
```

# Ownership

- Rust wants you to build safe programs
	- No memory leaks
	- Memory control / access only what is allowed
	- undefined behavior
	- error handling
- Rust does not have a Gargabe Collector (GC is costly)
- 