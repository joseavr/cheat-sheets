# Untitled

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-08-29

---

# Intro 

- Languages used to correct software
- Also called Proposional Logic
- Components of Symbolic Logic
	- Syntax: how formula looks like, sequence of formula is well formed
	- Semantics: what formulas mean
	- Proof system: how to do proofs
		- Axioms: assumed to be true
		- Inference rules:


# Proposional Calculus

Syntax
```haskell
p:= p        variables
	| (~p)      negation
	| (p v p)   disjunction
```

- Convention
	- Parenthesis often omitted
	- ~p v q means ((~p) v q)

## Derived Operators
- tt -> 'true' -> p v ~p
- ff -> ~tt
- p ^  q -> ~ ( (~p) v (~q) )  -> Morgan Law
- p => q -> (~p) v q
- p <=> q -> (p v q) v (~p ^ ~q)


## Semantics of Prop. Calculus

Able to say when formulas are true / false

is p v q true or false?
Cant't tell. Need truth values of p, q.

## States

- Mapping from variables to B = {0 , 1}  "Booleans"

- Mathematically, `states` is a table

| p   | B   |
| --- | --- |
| p   | 0   |
| q   | 1   |

Given as a relation  p |= q
p (state)
q (formula)

`Idea`:  p |= q holds when p "makes q true"
State is on the left
Formula is on the right
