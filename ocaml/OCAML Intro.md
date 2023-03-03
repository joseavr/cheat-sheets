Í# OcamL
Class: [[OCAML]]
Subject: #
Date: 2023-02-14
Topics: #, #, # 

---

# Intro to OCAML
- OCaml uses static and latent typing
- Variables in OCaml are immutable
- Since variables are immutable, they cannot be overwritten by variables
	- Once a variable is assigned a value, it cannot be changed
```ocaml
let x = 5;;
print_int x;; (* Output: 5 *)

x = 10;; (* Error: This expression has type int but an expression was expected of type unit *)
```

## OCAML ENV
- ocaml: `repl` like `irb`
- utop: like `ocaml` but better
- `dune` like `Make`
- `opam` package manager for OCaml
- To run
	- `dune utp src`
# Declarative vs Imperative

## Imperative
- Imperative instructions tell you how to do something and does so in steps

```ruby
# imperative.rb
results = []
arr.each{|item|
	remainder = item % 2 
	if remainder == 0
		results.push(0)
	end
}
results
```

## Declarative
- The declarative instructions tells you what you are looking for and assumes you can just figure out how to do it.
```ruby
# declarative.py
results = [x for x in arr if x % 2 == 0]
```

# Side Effects

$f ( x ) + f ( x ) + f ( x ) = 3 * f ( x )$

- However, if we run the code above, then 
- $f(x) + f(x) + f(x) = 1 + 2 + 3$ and $3 * f(x) = 3 * 1$. 
- This unpredictability is called a side effect 
- The true definition of a side effect is when non local variables get modified

# Expression in OCAML
- In OCaml, we say that almost everything is an expression
- All values are expressions in and of themselves, but not all expressions are values.


```ocaml
(* expressions.ml *)
true (* is a value, has type bool *)
3 * 4 (* is an expression, has type int *)
"hello" ^ "world" (* is an expression of type string *)
5.4 (* a value of type float *)
```

- There are things not consider an expression: the binding of expressions to variables
- A `let`binding is not an expression and just binds an expression to a variable. Here is an example:
```ocaml
(* letBinding.ml *)
let x = 3 + 4
(* syntax *)
(* let variable = e*)
```

- A let expression is like setting a local variable to be used in another expression
```ocaml
(* letExpression.ml *)
let x = 3 + 4 in x + 1 
(* syntax *) 
(* let variable = e1 in e2 *)
```

- Since immutable in OCaml, variables are overwritten.

```ocaml
(* scoping.ml *)
let x = 3 in let y = 4 in x + y (* 7 *)
let x = 3 in let x = 4 in x (* 4 *)
let x = 3 in let z = 4 + x in let x = 1 in x + z (* 8 *) 

(* implicit parenthesis *)
let x = 3 in (let z = 4 + x in (let x = 1 in x + z))
```

- Another kind of expressions
```ocaml
let x = if true then false else true in let y = 3 + 4 in let z = if true then 2 else 6 in if x then y else z
```

```ocaml
(* implicit parenthesis *) 
let x = (if true then false else true) in let y = (3 + 4) in let z = (if true then 2 else 6) in (if x then y else z)
```

## The IF expression

```ocaml
(* RULE FOR IF EXPRESSIONS*)
( if e1:bool then e2:t e3:t ):t (* where t : datatype and e : expressions*)
```
- e1 must evaluate to `bool`
- e2 and e3 must be the same datatype `t`

## Valid Expressions
- Unlike Ruby or other programming languages,
	- `true` and `false` or expressions that evaluate to `true` or `false` are only allowed in `if`
```ocaml
if true then 3 else 4

if true then false else true

if 3 < 4 then 5 + 6 else 7 + 8

if (if true then false else true) then (if false then 3 else 4) else (if true then 5 else 6)
```

- We can use `let` bindings and `let` expressions
```ocaml
let x = if true then false else true
let y = 3 + 4 - 10 in if true then y else y + 10
```

## Invalid Expressions

```ocaml
if 3 then 4 else 5
```

# The Function expression

- In ruby,
```ruby
x = 3
puts x 3
```

```ruby
def x 
	3
end
puts x
```

- In Ocaml,
```ocaml
(* functions.ml *)
let area l w = l * w 
(* or to use a let expression where we call the function *)
let area l w = l * w in area 2 3

(* syntax *)
(*  (let name e1:t1 e2:t2 ... ex:tx = e:ty):t1 -> t2 -> tx -> ty  *)
```

# Chaining
- The order of evaluation is "left-to-right"
```ocaml
let x = 1 in let x = x+2 in let x = x+3 in x

(* returns 6 *)
```

- It is equivalent to
```ocaml
 let x = 1 in let y = x+2 in let z = y+3 in z;;
```

- Can be rewriten as
```ocaml
(fun x -> let x=x+2 in let x=x+3 in x) 1
```

- Which is the same as
```ocaml
let x=1 in let y=x+2 in let z=y+3 in z
```