# OCAML Trees
Class: [[OCAML]]
Subject: #
Date: 2023-03-02
Topics: #, #, # 

---

# Intro to Trees

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