# 🐫 OCAML Variants
Class: [[OCAML]]
Subject: #
Date: 2023-03-09
Topics: #, #, # 

---

# 🎬 Intro to Variants
In OCaml, a variant type (a.k.a algebraic data type) allows you to define a type that can take on different forms. 

It's similar to an enumeration type in other programming languages, but with added flexibility. 

# 📏 Rule
A variant type is defined by 
- using the `type` keyword, 
- followed by the name of the type and 
- the different constructors that can be used to create values of that type.

# ✏️ Example
## Defining
Here's an example of a variant type in OCaml that represents different shapes:
```ocaml
type shape =
  | Circle of float
  | Rectangle of float * float
  | Triangle of float * float * float
```
- In this example, `shape` is the name of the variant type. 
- The constructors are `Circle`, `Rectangle`, and `Triangle`, each of which takes a different set of arguments.

## Initializing
With this definition, we can create values of type `shape` using the constructors:
```ocaml
let circle = Circle 3.14
let rectangle = Rectangle (4.0, 5.0)
let triangle = Triangle (3.0, 4.0, 5.0)
```

- In this example, `circle` has the value `Circle 3.14`, a circle with a radius of 3.14.
- `rectangle` has the value `Rectangle (4.0, 5.0)`, which is a rectangle with width 4.0 and height 5.0
- `triangle` has the value `Triangle (3.0, 4.0, 5.0)`, which is a triangle with sides of length 3.0, 4.0, and 5.0