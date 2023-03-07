# 🐫 OCAML High-Order Functions
Class: [[OCAML]]
Subject: #
Date: 2023-02-24
Topics: #, #, # 

---

# 🗺️ Map
- map returns a list of same length of `lst`
- The `map` function takes two arguments:
	- a function `f` of type `'a -> 'b`, 
	- a list of type `'a list`. 
- It applies the function `f` to every element in the input list, and returns a new list of type `'b list` that contains the results.
## Rule
```ocaml
List.map func lst
```

```ocaml
func = (fun x -> do_smth)
```
- At each iteration, it replaces `each` from list with
	- fun x 

## Map Function
```ocaml
let rec map f lst =
	match lst with
		[] -> []
		h::t -> (f h)::(map f t)
```

## Non Map Function
```ocaml
let rec add1 xs ->
	match xs with
		[] -> []
		| ht::t -> (h+1)::(add1 t)
``` 

## Example
- The `map` function is typically implemented using recursion. Here is an example implementation of `map` using recursion
```ocaml
let xs = [1; 2; 3] 
let ys = map (fun x -> x * 2) xs 
(* ys = [2; 4; 6] *)
```

# 📁 Fold
- Iterates over a list and do somthing on the list
- It can return anything
- Kinda like a for loop

## ↩ Fold Left
### Rule
- `func` is a lambda function that combines the current value with the next element in the list
- `initial_value` is the initial value of the accumulator
- `list` is the list to be iterated over
```ocaml
List.fold_left func initial_value list
```

```ocaml
func = (fun acc x -> do_smth)
```
- At each iteration, it combines
	- `acc` previous value with
	- `x` current value
- `acc` will be returned

### Implementation
```ocaml
lst = [1;2;3;4]
(* a = accumulator *)
let rec fold f a lst =
	match lst with
		[] -> a
		| h::t -> fold f (f a h) t

(1+2(3+4))
```

### Example
```ocaml
let lst = [1; 2; 3; 4; 5]
let sum = List.fold_left (fun acc x -> acc + x) 0 lst
(* Output: sum = 15 *)
```


## ↪ Fold Right
### Rule
```ocaml
List.fold_right func list initial_value
```

```ocaml
func = (fun acc x -> do_smth)
```
- `acc` will be returned

### Implementation
```ocaml
[1;2;3;4]
let rec fold_right f lst a = 
	match lst with
		[] -> a
		| h::t -> f h (fold_right f t a)

((4+3)+2)+1)
```

### Example
```ocaml
let lst = ["hello"; "world"; "!"] 
let concat = List.fold_right (fun x acc -> x ^ acc) lst "" 
(* Output: concat = "helloworld!" *)
```