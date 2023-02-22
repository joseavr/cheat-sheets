# OCAML Functions
Class: [[OCAML]]
Subject: #
Date: 2023-02-22
Topics: #, #, # 

---

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
	|h::t -> h*(product)
```

## Power
```ocaml
let rec pow x p = match p with
  | _ when p = 0 -> 1
  | _ -> x * pow x (p-1)
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
	if n = 0 then 
		a 
	else 
		fib (n-1) (a+b) a;;
```

## Factorial
```ocaml
let rec factorial n =
	if n == 0 then
		1
	else n * factorial(n-1);;
```

## Is Prime
```ocaml
let is_prime n = 
	let rec nonDivisble num next = match next with
	| 1 -> true
	| _ -> (num mode next <> 0) && nonDivisible num (next-1)
	in
	match n with
	| _ when x < 0 -> false
	| 0 | 1 -> false
	| _ -> nonDivisible n (n-1);;
	
```

## Primes
```ocaml
let rec prime_values lst = match lst with
	[] -> []
	| h::t -> if is_prime h then h::(prime_values t) else prime_values t
```