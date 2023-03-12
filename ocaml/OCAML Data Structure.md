# 🐫 OCAML Data Structure
Class: [[OCAML]]
Subject: #
Date: 2023-02-17
Topics: #, #, # 

---

# 🎬 Intro 

```ocaml
let x = 5 in let y - 2 in x + y;;;
(* 5 = y -2*)
(* y = 2*)
(* x = 5+2*)
```


# 1️⃣ Functions
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

## Defining a Type of a Function
- The general pattern for determining the type of any function is:
- `'a`  means that can be any data type
```ocaml
first_param_type -> second_param_type -> ... -> last_param_type -> return_type`
```

- To make return type a boolean, we use an if-statement
```ocaml
'a -> 'a -> bool

let func a b =
	if a = b then
		false;;
```


- Show ('a -> 'b) takes type `a` and `b`
```ocaml
('a -> 'b) -> 'a -> 'b -> bool

let func g a b = 
	if (g a)
		b
	then 
		true;;

let func f a b = (f a) = b;;
```

```ocaml
int -> (int -> float) -> string

let func i f = 
	if (f (i+1)) = 2.0 then
		"e" 
	else 
		"a"

Conversion functions:
float_of_int n
string_of_float n

int -> int -> float list
let func i1 i2 = [float_of_int(i1+1); float_of_int(i2+1)]

```

## Recursive
- Use `rec` keyword
```ocaml
let rec func a = (func a);;
```

# 2️⃣ List
```ocaml
let my_list = [1;2;3];;
```

```ocaml
let my_second_list param_a param_b = [param_a; param_b] in my_second_list 1 2;;
```

## `cons` operator `::`
- Rule
	- `element`::`List`
```ocaml
1::[1;2]
=> [1;1;2]
```


```ocaml
('a -> 'b) -> 'a -> 'b list -> 'b list

let func f a b_list = (f a)::b_list
```

## `preppend` operator `@`
- Rule
	- `List@List`


# 3️⃣ Tuples
TODO

# 4️⃣ Pattern Matching
-  It's like regular expressions for values. Match against desired value

``` ocaml
let lst = [1;2];;

match lst with
| [] -> []
| h::t -> h
```

```ocaml
let lst = [1;2;3;4];;

let rec sum lst =
match lst with
| [] -> []
| h::t -> h + (sum t) (*recursively call sum with the tail of the list t*)
```
