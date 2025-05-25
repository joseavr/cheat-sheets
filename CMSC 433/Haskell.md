 📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-10-19

---

# Intro 
- Strong typed language. 
- Static typed, type checking done at compile time
- Types are polymorphic
- Functional programming language. Mainly uses functions. Can be used as variables and passed as arguments.
- Avoids mutable data, once variable is defined then it cannot be changed.
- Recursion (similar to Ocaml)

Compile: 
```bash
ghc {file-name}.hs
```

Run program (excutable):
```bash
./{file-name}
```

Haskell Playground:
```bash
ghci
```

# Notes

- A string is a considered as type list []

# Examples

#### head
```haskell
head "abc"
-> 'a'
```

#### tail
```haskell
tail "abc"
-> "bc"
```

#### concat
```haskell
"aaa" ++ "bbb"
-> "aaabbb"
```

# Check Types
We can check the type of haskell operators with `:t`

```haskell
:t (++)
(++) :: [a] -> [a] -> [a] 
```

- (++) operator that takes two lists, both of type [a]
- concats them to make a new list of same type [a]
