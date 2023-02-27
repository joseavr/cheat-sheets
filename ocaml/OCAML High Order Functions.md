# OCAML High-Order Functions
Class: [[OCAML]]
Subject: #
Date: 2023-02-24
Topics: #, #, # 

---

# Map
- map returns a list of the same size
- The `map` function takes two arguments:
	- a function `f` of type `'a -> 'b`, 
	- a list of type `'a list`. 
- It applies the function `f` to every element in the input list, and returns a new list of type `'b list` that contains the results.

## What looks like
```ocaml
let rec add1 xs ->
	match xs with
		[] -> []
		| ht::t -> (h+1)::(add1 t)
```

```ocaml
let rec square xs =
	match xs woth
		[] -> []
		| h::t -> (h*t)::(square t)
```
## Map Function
```ocaml
let rec map f lst =
	match lst with
		[] -> []
		h::t -> (f h)::(map f t)
```
## Example
- The `map` function is typically implemented using recursion. Here is an example implementation of `map` using recursion
```ocaml
let xs = [1; 2; 3] 
let ys = map (fun x -> x * 2) xs 
(* ys = [2; 4; 6] *)
```

# Fold
- Iterates over a list and do somthing on the list
- It can return anything
- Kinda like a for loop

- Suppose
```ocaml
xs = [1;2;3;4]
let rec sum xs ->
	match xs with
		[] -> 0
		| h::t -> h+(sum t)

(1+2(3+4))
```
- What is the difference with?

```ocaml
let rec size xs = 
	match xs with
		[] -> 0
		| h::t -> 1+(size t)
```

## Fold Left
```ocaml
lst = [1;2;3;4]
(* a = accumulator *)
let rec fold f a lst =
	match lst with
		[] -> a
		| h::t -> fold f (f a h) t

(1+2(3+4))
```

## Fold Right
```ocaml
[1;2;3;4]
let rec fold_right f lst a = 
	match lst with
		[] -> a
		| h::t -> f h (fold_right f t a)

((4+3)+2)+1)
```

# Tree Type

- Tree data type, any other type
```ocaml
type `a tree =
	| leaf
	| Node of `a tree * `a * `a tree
```

- Recursively defines a `tree` to be
	- `Leaf`
	- `Node` with left sub-`tree`, a value, and a right sub-`tree`