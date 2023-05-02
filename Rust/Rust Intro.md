# 🦀 Rust Intro

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-04-27

---

# 🎬 Intro to Rust
- Security
- Memory Control like in C
- Rust says no Gargabe Collector

# Stack - Automatic
- Programmers doesn't have to deal with
- Variables stored in the stack automatically
- Fixed size: Define how much memory to allocate in the stack
- Lifetime: How long is a something (variable, function, etc) is gonna stay in memory.


# Heap - Memormy Managment
- Dynamic size
- No fixed scope

# No Garbage Collector
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

- Dangling Pointer: Trying to use a pointer outside of scope

# How Rust Fix These Issues
- Rust forces safe programs via **Type** system
	- Variables with specified types: Int, Float, String, etc
- Rust also forces saf programs thru enforcing
	- Ownership
	- Lifestime
- It is very hard to write safe programs

## Ownership
What is Ownership?
- Data has single owner (who can manipulate this single data)
- Immutable aliases allowed
- Mutation only has 1 reference

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

### Functions?
- There are 3 ownership happening in this piece of code
```rust
{
  let s = String::frin("Hello") // 1. s is owner
  let y = identity(s); // 3. x losses ownershi[, y is now the owner
  println!(y)
}

fn identity(x: String) -> String {
  x // pushed in the stack, s losses ownership, 2. x is now the owner
}
```

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

### Borrowing
- Send a temporary anothership to another variable
- When the owner dies, get the ownership back to the inital borrower
```rust
let l = get_len(*s)

fn get_len(x:&String) -> usize {
  x.len
}
```

**Rules**:
- Can have one, but not both of the following at the given time
	- 1.a. One mutable reference exist
	- 1.b. Infinitely many immutable ref exist
	- 2.a. All references myst be valid

```rust
// fails because rule 2
let s  = String::from("Hello")
let s1 == &s;
let s2 = &s;

let s3 = &mut s;
```

### Deep Copy?
```rust
let y = identity( s.clone() )
```



## Lifestimes
What is Lifestime?
- 


## Mutability
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