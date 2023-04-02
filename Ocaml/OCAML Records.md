# 🐫 OCAML Records

📚Class: CMSC 330 Organization of Programming Languages 

📓Subject: OCAML 

✏️Section: 0105 

📅Date: 2023-02-27

---

# 🎬 Intro to Records
Records aka Objects

# 🔎 Extract Fields from Records

## Declaring and Initializing
```ocaml
type person = { name : string; age : int; email : string option }

let alice = { name = "Alice"; age = 30; email = Some "alice@example.com" }
```

## Extract Fields
In OCaml, we can extract fields from a record using `let` and pattern matching
```ocaml
(* RULE *)
let {field1, field2} = Object
```

```ocaml
let { name; age } = alice in
Printf.printf "Name: %s, Age: %d\n" name age

=> Name: Alice, Age: 30

```
## Extract Fields 2
If we wanted to extract `email`
```ocaml
let { name; age; email } = alice in
match email with
| Some e -> Printf.printf "Name: %s, Age: %d, Email: %s\n" name age e
| None -> Printf.printf "Name: %s, Age: %d, No email\n" name age

```

# 🧑🏻‍💻 Example
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