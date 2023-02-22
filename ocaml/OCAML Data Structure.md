# Ocaml Data Structure
Class: [[OCAML]]
Subject: #
Date: 2023-02-17
Topics: #, #, # 

---

# Intro 

-

```ocaml
let x = 5 in let y - 2 in x + y;;;
(* 5 = y -2*)
(* y = 2*)
(* x = 5+2*)
```


# Functions
```ocaml
let func a = a;;
(* return a*)
```

- cant use the keyword `fun`

```ocaml
let func a b = a + b;;

(* int -> int -> int *)
```

```ocaml
(* Rule: if boolean then t else t *)
let check_empty_string str_param = 
    if str_param = "" then true else false;; (* type: string -> boolean *)

let check_a_string str_param = 
    if str_param = "a" then true else "invalid string";; (* will fail to compile *)
```

# Defining a Type of a Function
- The general pattern for determining the type of any function is:

```ocaml
first_param_type -> second_param_type -> ... -> last_param_type -> return_type`
```

- $'$  following a variable means that can be any data type

- To make now the type is a boolean, we use an if-statement
```ocaml
(* 'a -> 'a -> bool` *)

let func a b =
	if a = b then
		false;;
```


- Show ('a -> 'b) takes type `a` and `b`
```ocaml
(* ('a -> 'b) -> 'a -> 'b -> bool` *)

let func g a b = 
	if (g a)
		b
	then 
		true;;

let func f a b = (f a) = b;;
```

```ocaml
(* int -> (int -> float) -> string *)

let func i f = if (f (i+1)) = 2.0 then "e" else "a";; 

float_of_int 
string_of_float
```

# Recursive
- Use `rec` keyword
```ocaml
let rec func a = (func a);;
```



# List
```ocaml
let my_list = [1;2;3];;
```

```ocaml
let my_second_list param_a param_b = [param_a; param_b] in my_second_list 1 2;;
```

## `cons` operator `::`
- Rule: `element`::`List`
```ocaml
1::[1;2]
=> [1;1;2]
```

```ocaml
(* int -> int -> float list *)
let func i1 i2 = [float_of_int(i1+1); float_of_int(i2+1)]
```

```ocaml
(* ('a -> 'b) -> 'a -> 'b list -> 'b list *)

let func f a blist = (f a)::blist;; 
```

# Pattern Matching

-  It's like regular expressions for values. Match against desired value
``` ocaml
let lst = [1;2];;

match lst with
| h::t -> h
| [] -> []
```

```ocaml
let lst = [1;2;3;4];;
let rec sum lst =
| h::t -> h + (sum t) (*recursively call sum with the tail of the list t*)
| [] ->
match 
```


# Map

```ocaml  
let rec map f l = match l with
[]-> []
|h::t -> (f h)::(map f t)

map: ('a -> 'b) -> 'a list -> 'b list
```

```ocaml
[1,2,3,4]

#Recursion1
h=[1]
t=[2,3,4]

#Recursion2
f (h)
h=[]
t=[1]

#Recursion3
f(h)
=>[]

#Recursion4 (map f t)


```

## Example
```ocaml
let add1 x = x + 1;;
let x2 x = x + x;;
let is_even x = x mod 2 = 0;;
let lst = [1;2;3];;

map add1 lst;;
map x2 lst;;
map is_even lst;;

let fs = [add1;x2;(fun x -> -x)]
map (fun f -> map f lst) fs;;
```

# Useful Functions With MAP
## Concat
```ocaml
let rec concat lst = match lst with
[]-> ""
|h::t -> h^(concat t)
```

## Sum

```ocaml
let rec sum lst = match lst with
[]-> 0
|h::t -> h+(sum t)
```

## Product
```ocaml
let rec product lst = match lst with
[]-> 1
|h::t -> h*(productt)
```

## Length
```ocaml
let rec length lst = match lst with
[]-> 0
|_::t -> 1+(length t)
```

## Reverse
```ocaml
let rec rev lst = match lst with
[]-> []
|h::t -> (rev t) @ [h];;
```

## Filter
```ocaml
let rec filter lst compare_fun = match lst with
[]-> []
|h::t -> if compare_fun h then
h::(filter t compare_fun) else filter t compare_fun;;
```

## Fibonacci
```ocaml
(* fib-1.ml *)
let rec fib n a b =
if n = 0 then a else fib (n-1) (a+b) a;;
```

# Fold
- Fold will incorporate
- Aggregating a list to a single value
- Reducing Stack Frames
```ocaml
(* fold.ml *)
let rec fold f a l= match l with
[]-> a
|h::t-> fold f (f a h) t;;

fold: ('a -> 'b -> 'a) -> 'a -> 'b list -> 'a
```

# Foldr
- Aggregating a list to a single value
- But, the order of evaluation is reversed
```ocaml
(* foldr.ml *)
let rec foldr f l a = match l with
[]-> a
|h::t-> f h (foldr f t a);;

foldr: ('b -> 'a -> 'a) -> 'b list -> 'a -> 'a
```
# Map & Fold
```ocaml
(* count 1s in a 2d matrix *) 
(* based on what we already have (inefficent) *) 
let countones lst = 
(* take out non-ones from 1-d list *) 
let get1s lst = filter (fun x -> x = 1) lst in 
(* take out non-ones from each sublist *)
let ones = map get1s lst in 
(* get the length of each 1 list *) 
let counts = map (fold length 0) ones in 
(* add up the lengths *) 
let total = fold sum 0 counts in total;;
val countones : int list list -> int = 

(* or we can do the easy way *)
let count1 lst = fold (fun a h -> if h = 1 then a+1 else a) 0 lst;;
let count1s lst = fold (+) 0 (map count1 lst)
```

