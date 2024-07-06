# 🐫 OCAML Functions

📚Class: CMSC 330 Organization of Programming Languages 

📓Subject: OCAML 

✏️Section: 0105 

📅Date: 2023-02-22


---

# ✅ Useful Functions

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
	|h::t -> h*(product t)
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

## Last Element of a List
```ocaml
let rec last l = 
	match l with 
	| [h] -> h 
	| (h::t) -> last t
```

## Split List
```ocaml
let rec splitList lst empty depth = 
	if depth = 0 then 
		(lst, empty)
	else 
		match lst with 
			| [] -> ([], []) 
			| hd::tl -> splitList tl (hd::empty) (depth - 1)
```

```ocaml
let rec split_at_point lst n =
    if n = 0 then
        (* Answer is obvious *)
    else
        match lst with
        | [] -> (* Answer is obvious *)
        | head :: tail ->
            (* Call split_at_point on the tail and
             * construct your answer
             *)
```

## Fibonacci
```ocaml
(* Fibonnaci sum at term n *)
let rec fib n = 
  if n = 1 || n = 0 then n 
  else fib (n - 1) + fib (n - 2)
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


## Same_Length

```ocaml
let same_length lst1 lst2 =

  let len1 = length lst1 in

  let len2 = length lst2 in

  let count = ref 0 in

  if len1 > len2 then

    fold (fun acc e -> if !count < len2 then (count := !count + 1; e::acc) else acc) [] (lst1)

  else

    lst1
```

## Partition Sum
- Return a tuple where
	- first element is the sum of even indices
	- second is the sum of odd indices
	- thrid is the length of the list

partition_sum $[1;2;3]$ = (4,2,3) 
partition_sum $[2;5;6;8]$ = (8,13,4)

```ocaml
let partition_sum lst = 
	fold_left 
	(
		fun acc x -> match acc with
			| (even,odd,len) -> 
				if len mod 2 = 0 then
					(even+x, odd, len+1)
				else 
					(even, odd+1, len+1)
	) 
	(0,0,0) 
	lst
```

## Take
- Return a list with a specific length

take 3 $[1;2;3;4;5]$ = $[1; 2; 3]$

```ocaml
let rec take n lst =
  match n, lst with
  | 0, _ -> []
  | _, [] -> []
  | n, h::t -> h::take (n - 1) t
```


## Drop
- Return a list without the first `n` elements

drop 3 $[1;2;3;4;5]$ = $[4;5]$
```ocaml
let rec drop n lst =
	match n, lst with
	| 0, lst -> lst
	| _, [] -> []
	| n, h::t -> drop (n - 1) t
```


## Unique List
- Returns an unique List from a list as input 

unique_list $[1;0;1;0]$ = $[1;0]$
```ocaml
(* count_occurrence [1; 2; 2; 1; 3] 1 => 2 *)
let count_occ lst target =
	fold (fun acc e -> if e = target then acc+1 else acc) 0 lst

(* unique_list [1;2;2;1;3] => [2;1;3]*)
let unique_list lst =
	fold (fun acc e -> if (count_occ acc e) > 0 then acc else e::acc) [] (lst)
```