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
let rec fold f acc lst =
	match lst with
		[] -> acc
		| h::t -> fold f (f acc h) t
```

### Example
```ocaml
let lst = [1;2;3;4;5] 
let sum lst = List.fold_left (fun acc x -> acc - x) 0 lst

Return:
(((((0-1) -2) -3) -4) -5) = -15
```


## ↪ Fold Right
### Rule
```ocaml
List.fold_right func list initial_value
```

```ocaml
func = (fun x acc -> do_smth)
```
- `acc` will be returned

### Implementation
```ocaml
let rec fold_right f lst acc = 
	match lst with
		[] -> acc
		| h::t -> f h (fold_right f t acc)
```

### Example
```ocaml
let lst = [1;2;3;4;5] 
let concat = List.fold_right (fun x acc -> x - acc) lst 0 

Returns:
(1 - (2 - (3 - (4 - (5 - 0)))))
```


# ✅ Useful Functions

## `get_every_kth` (tuple and counter)
- Returns the a list of every multiple of 2 indexes
get_every_kth 2 [1;2;3;4;5] = [2;4]
get_every_kth 3 [1;2;3;4;5;6;7;8;9;10] = [3;6;9]
```ocaml
let get_every_kth n lst =
	let ( _ , result) =   (* Destructuring tuple *)
		List.fold_left 
		( fun (c, acc) e ->
		if c mod n = 0 then
			(c+1,e::acc)
		else
			(c+1,acc)
		)
		(1, [])  (* counter + accumulator *)
		lst

	in result   (* returning accumulator *)    
```

## `neighbor_value` (Nodes and Graph DataStructure)
- Given a `graph` and `node`
```ocaml
type node = Node of int;;
type graph = (node * node list) list;;
```
- Returns a list of tuples, where each tuple is (node value, sum of neighbors)
- Example
```ocaml
g = [
	(Node(1) , [Node(2) ; Node(3)]) ; 
	(Node(2) , [Node(3)]) ; 
	(Node(3) , [Node(1) ; Node(3)])
	]
	
neighbor_value g = [(1,5) ; (2,3) ; (3,4)]
```


- `neighbor_value g`
```ocaml
let neighbor_value g = 
(* fold to sum neighbors of a Node *)
	let sum_neighb lst = 
		List.fold_left 
		(fun acc e ->
			let Node v = e (* Retrieve value of Node *)
			in v + acc	
		)
		0
		lst
	in 
(* fold each tuple from Graph *)
	List.fold_left 
	(fun acc (v,neighbors) -> (* Destructuring each tuple from g *)
		let Node vl = v in    (* Retrieve value of Node *)
		(vl , sum_neighb neighbors)::acc
	)
	[]
	g

```