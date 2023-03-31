# 🐫 OCAML Conditions

📚Class: CMSC 330 Organization of Programming Languages 

📓Subject: OCAML 

✏️Section: 0105 

📅Date: 2023-03-06

---

# 🎬 Intro to Conditions
- Let's say our database has
```ocaml
let db1 =  [
				{name="Alice";age=23;hobbies=["Skiing";"golfing"]}; 
				{name="Bob";age=42;hobbies=["Skiing";"Cooking"; "Legos"]}
			]
```

## 1️⃣ Age, Name, Hobbies Condition
- We want to return a list from our `db` according to a given `condition`
- Where Age of each `person` is greater than 30
```ocaml
let condition = Age (fun x -> x > 30) 

query condition db1 = 
	[{name="Bob";age=42 ; hobbies=["Skiing";"Cooking"; "Legos"]}]
```


### Solved
```ocaml
let rec query condition db =
	match condition with
	| Age func -> List.filter (fun person -> func person.age) db
```
- `List.filter fun lst`: 
	- Takes each element of `lst` that meets up the conditions defined by `fun` into a new list
	- Returns a new list

## 2️⃣ AND - Condition
- We want to return a list from our `db` that matches both `condition1` and `condition2`
```ocaml
let condition = And(Age(fun age -> age > 30), Name(fun name -> name = "Bob"));;

query condition db1 = 
	[{name="Bob";age=42}]
```

### Solved
```ocaml
let rec query condition db = 
	| And (c1, c2) -> 
		List.filter 
		(
			fun person -> 
				List.mem person (query c1 db)
				&& 
				List.mem person (query c2 db)
		)
		db
```
- `List.filter fun db`: returns a `list` of all person from `db` that matches with query `fun`
- `fun person -> `
	- `List.mem person (query c1 db)`: evaluates if `person` is in the query of `c1`
		- If `person` is in query, returns `True`, continues to next query
		- If empty, returns `False`, therefore the condition returns a empty list `[]`
	- `&& List.mem person (query c2 db)`: evaluates if `person` is in the query of `c2`
		- If `person` is in query, returns `True`, therefore the `person` is added to `list`
			- returns the `list` of `person`'s which both conditions meet 
		- If empty, returns `False`, returns a empty list `[]`

## 3️⃣ OR - Condition
- We want to return a `list` of all persons from our `db` that matches either `condition1` or `condition2`
```ocaml
let condition = And(Age(fun age -> age < 30), Name(fun name -> name = "Bob"));;

query condition db1 = 
	[
		{name="Bob";age=42} ; 
		{name="Alice";age=23}; 
	]
```

### Solved
```ocaml
let rec query condition db = 
	| And (c1, c2) -> 
		List.fold_left
		(
			fun acc person -> 
			
				if List.mem person acc
					then acc
				else 
					person@acc
		)
		[]
		( (query c1 db)@(query c2 db) )
```

- `List.fold_left`: will iterate each `person` from all persons that meets either `c1` or `c2` and will add non-repeated perons into `acc` to later return this accumulator
- `fun acc person ->`
	- `If List.mem person acc then acc`: If the person is already in the accumulator then do not add
	- `else person@acc`: if the person is not in the accumulator, then add to the list
- `[]`: initial value for the accumulator. An empty list for `person`'s that meets `c1` or `c2`
- `(query c1 db)@(query c2 db`: a list that meets either `c1` or `c2`


## 4️⃣ IF - Condition
- We want to perform a query based on and if-else statement
-  if true then Age else Name
```ocaml
let condition = If(True,Age(fun age -> a < 30) , Name(fun name -> name = "Bob"))

query condition db1 = 
	Age(fun age -> a < 30) = 
	[{name="Alice";age=23;hobbies=["Skiing";"golfing"]}]
```
- If `c1` is true
	- Perform `c2` and return the query that matches up 
- If `c1` is false
	- Perform `c3` and return the query that matches up

### Solved
```ocaml
let rec query condition db =
	match condition with
	| If (c1, c2, c3) ->
		List.fold_left
		(fun acc person ->
			if List.length (query c1 [person]) > 0 then
				(query c2 [person])@acc
			else
				(query c3 [person])@acc
		)
		[]
		db
```
- `List.fold_left`: traverse thru each element of `db` and add into the `acc` the persons that meets the criteria
- `if List.length (query c1 [person]) > 0`: If condition is true, meaning length of query is 1 because the person is matched
	- `then (query c2 [person]) @ acc`: evaluate this person with `condition2` and add it to `acc`. Adds either `[]` or `person`
	- `else (query c3 [person]) @ acc`: evaluate this person with `condition3` and add it to `acc`. Adds either `[]` or `person`