# 🐫 OCAML Operators
Class: [[OCAML]]
Subject: #
Date: 2023-02-22
Topics: #, #, # 

---

# Operators

| Operators       | Meaning                                                              |
| --------------- | -------------------------------------------------------------------- |
| `+`             | Integer addition                                                     |
| `-` (infix)     | Integer subtraction.                                                 |
| `~- -` (prefix) | Integer negation.                                                    |
| `*`             | Integer multiplication.                                              |
| `/`             | Integer division. Raise Division_by_zero if second argument is zero. |
| `mod`           | Integer modulus. Raise Division_by_zero if second argument is zero.  |
| `land`          | Bitwise logical “and” on integers.                                   |
| `lor`           | Bitwise logical “or” on integers.                                    |
| `lxor`          | Bitwise logical “exclusive or” on integers.                          |
| `lsl`           | Bitwise logical shift left on integers.                              |
| `lsr`           | Bitwise logical shift right on integers.                             |
| `asr`           | Bitwise arithmetic shift right on integers.                          |
| `+.`            | Floating-point addition.                                             |
| `-.` (infix)    | Floating-point subtraction.                                          |
| `*.`            | Floating-point multiplication.                                       |
| `/.`            | Floating-point division.                                             |
| `**`            | Floating-point exponentiation.                                       |
| `@`             | List Concatenation                                                   |
| `^`             | String Concatenation                                                 |
| `!`             | Dereferencing                                                        |
| `=`             | Structural Equality                                                  |
| `<>`            | Structural Inequality                                                |
| `==`            | Physical Equality                                                    |
| `!=`            | Physical Inequality                                                  |
| `<`             | Less than                                                            |
| `<=`            | Less than or Equal                                                   |
| `>`             | Greater than                                                         |
| `>=`            | Greater than or Equal                                                |
| `&&` `&`        | Boolean Conjunction                                                  |
| `or`            | Boolean Disjunction                                                                      |

# `When` keyword
Patterns can also incorporate conditions or _guards_ that impose restrictions on the match; these guards are introduced by the keyword when with the syntax: _pattern_ when _expr1_ -> _expr2_. _expr1_ is a Boolean expression (it can reference variables bound by the pattern) and the entire clause matches only if the guard is true. Here's a rewrite of the mem function using a guard:

```ocaml
let rec mem x list =
	match list with 
	| [] -> false
	| h::_ when h = x -> true
    | _::t -> mem x t
```


# `Ref` keyword

## How to count++ inside a statement

In the given OCaml code, the `count` variable is declared with an incorrect syntax. To declare and initialize a variable in OCaml, you can use the `let` keyword followed by the variable name, the `=` sign, and the initial value. Therefore, the correct syntax to declare and initialize `count` would be:

```ocaml
let count = ref 0 in
```

Note that we are using a reference type here instead of a regular integer type. This is because we want to modify the value of `count` inside the `fold` function.

To increment `count` inside the `fold` function, we can use the `:=` operator, which is the assignment operator for reference types. Therefore, the modified code would be:

```ocaml
let same_length lst1 lst2 =   
	let len1 = length lst1 in   
	let len2 = length lst2 in   
	let count = ref 0 in   
	if len1 > len2 then      
		fold (fun acc e -> 
				if !count < len2 then 
					(count := !count + 1; e::acc) 
				else 
					acc
			) 
			[] 
			(lst1)   
	else     
		lst1
```

`!count` to dereference the reference type and get the actual integer value. 
`count := !count + 1` statement inside the lambda function to increment `count` for each element that is added to the new list.