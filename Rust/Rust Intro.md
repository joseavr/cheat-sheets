# 🦀 Rust Intro

📚Class: CMSC 330 Organization of Programming Languages 

📓Subject: Rust 

✏️Section: 0105 

🗓️Date: 2023-04-27

---

# 🎬 Intro to Rust
- Security
- Memory Control like in C
- Rust says no Gargabe Collector
- Statically Typed
- Imperative Language
- Compiled Language
- Solves memory issues that C has
- Addresses issues such as dangling pointers, double free, data-races
- Syntax: like C and Ocaml
- Rust forces safe programs via its type system
```rust
3 + 4.0 // valid in Ruby and Rust, not in OCaml
```
- Rust forces safe programs thru
	- [Ownership](./Rust%20Ownership)
	- [Lifetime](./Rust%20Lifetime)

# [Rust Data Types](./Rust%20Data%20Types)

# Recap: Stack vs Heap
 - Memory on the stack (variables, functions) is automatically allocated and deallocated by the program as functions are called and return.
- In contrast, memory on the heap (objects) must be explicitly allocated and deallocated by the program using memory allocation routines, such as `malloc()` and `free()`.

# Stack - Automatic
- Programmers doesn't have to deal with
- Variables stored in the stack automatically
- Fixed size: Define how much memory to allocate in the stack
- Lifetime: How long is a something (variable, function, etc) is gonna stay in memory.


# Heap - Memormy Managment
- Manual memory managment
- Dynamic size
- No fixed size

# No Garbage Collector
- Rust tries to make heap memory managment like stack memory
- Rust says no Gargabe Collector

- Is there a issue in this block code? The code will compile, but in the scope we are mallocing in the heap and never deallocating, thus MemoryLeak
```rust
{ int *x = (int*) malloc(size of(int)); }  // memory Leak
```

- What if used a pointer after freed? 
```rust
{ in *x = malloc( size of(int) );
  ...
  free(x);
  ...
  *x = 5;
}
```

- Double free?
```js
{ in *x = malloc( size of(int) );
   free(x)
   free(x)
}
```
*Note: Dangling Pointer is when trying to use a pointer outside of scope*

# How Rust Fix These Issues
- Rust forces safe programs via **Type** system
	- Variables with specified types: Int, Float, String, etc
- Rust also forces saf programs thru enforcing
	- Ownership
	- Lifestime
- It is very hard to write safe programs

## Ownership

### **Rules**:
- Each `value` has a `variable` that is its owner
- Only one owner at a time
- In terms of memory, when `owner` out of scope, the `value` is dropped (freed)
```rust
{
let mut s = String::from("Hello");
s.push_str(", world");
println!("{}"s)
}
```

- Since we only can have one owner, `s` losses ownership, `y` takes ownership
- If we were to print `s`, no compile (rust yell us: it's unsafe!)
```rust
let s = String::from("Hello");
let y = s; // s transferred ownership to y (called move or 's' move to 'y')
println!("{}", y); // good
printl!("{}", s); // error
```
Note: this is a shallow copy
Note: cannot take ownership back to `s` ( `s = y` ) unless we do another `let s = y`


### Owner Out of scope Issue
```rust
{
  let s = String::from("Hello")
  let l = get.len(s)
  println!({} is [} long, S, L)
}

fn get.len(x:String) -> usize {
  x.len()
}
```

- To solve this issue: Tuple, Borrowing (correct approach)



## Lifestimes
What is Lifestime?
- 


# Mutability
- Use keyword `mut` 
- `mut` means the value is mutable
- It can change the value, but not what the variable is point to
```rust
let mut s = 5;
s = s + 1; // 6, allowed to mutate
```

```js
let b = s
b.push_str("World") // fails because b is not mutable
```