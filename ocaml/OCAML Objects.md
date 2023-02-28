# OCAML Objects
Class: [[OCAML]]
Subject: #
Date: 2023-02-27
Topics: #, #, # 

---

# Intro to Objects


## Example

```ocaml
type course = { name: string
				; credits: int
				; students: string list 
			} ;;

let course = { name = "CMSC330"
			; credits = 3
			; students = ["student1"; "student2"] 
			} in
let { name; credits = c } = course in 
(name, c)
```

- Here is how it works:
1.  The `course` value is defined with an object type called `course` with
	- `name` = "CMSC330" 
	- `credits` = 3
	- `students` = `["student1"; "student2"]`.

3.  The `let { name; credits = c } = course` line uses pattern matching to extract
	- `name` field from `course`
	- `credits` field from `course`
	 Then binds them to the variables `name` and `credits`, respectively. 
	 
	 Note :
	- `credits = c` binds the value of `credits` to a new variable `c`.

5.  Finally, the `(name, c)` expression creates a tuple with the `name` and `c` values, which evaluates to `("CMSC330", 3)`.