# Dafny Programming

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-09-14

---

# Intro 

- Precondition: inputs allowed to provide
- Postcondition: specifies what user expects when code termines

```java
method Min(x: int, y: int) returns (min :int) // another way to return
	//requires true // Precondition; could be left out here since 'true'
	ensures min <= x && min <= y // Postcondition, statement that should hold
	ensure min == x || min == y // can break down for readibility
{
	if (x < y) {
		min := x; // could also use 'return'
	}
	else {
		min := y; // could also assign to min
	}
}
```


```java
method Abs(r: real) return (absR : real) 
	require true
	ensures absR >= 0.0
	ensures absR == r  || absR == -r  // relationship btw input and output
	// if initial arg is negative, should return positive. and viceversa
{
	if r < 0.0 {
		absR := -r;
	} 
	else {
		abs R := r;
	}
}
```


```java
method FindMInVal( a : array<int> ) returns (min : int) 
// Precoidntion, guarantees incoming arg. > 0 so a[0] should not fail
requires a.Length > 0 
// Postcondition
ensures forall  i : int :: 0 <= 1 < a.length ==> min <= a[i]
// for all i which is int
// must satisfies 0 <= i < a.length which is a valid index
// then min must be <= a[i]

{
	min := a[0];
	var i: = 1;
	while ( i < a.Length)
	{
		if a[i] < min
		 { min := a[i];}
		 i := i + 1
	}
}
```


## Annotations

- To know what is to be true at certain part of the code
- `ensures` and `requires` can have expressions that returns `boolean`: for loop, if satement.
- Precondition and Postconditions are not run in runtime
- if `requires` is specified then assume it must be true at the begining of the method
```java
method Min(x: int, y: int) returns (min :int) // another way to return
	requires true // Precondition
	ensures min <= x && min <= y // Postcondition, statement that should hold
	ensure min == x || min == y // can break down for readibility
{
	assert true; // annotation: reveals behavior of the program
	if (x < y) {
		assert x < y; // annotation
		min := x;
		assert min == x; // annotation
		assert min < y; // annotation
	}
	else {
	  assert x > y; // annotation
		min := y;
		assert min == y; // annotation
		assert min <= x; // annotation
	}
	assert min == x || min == y; // annotation
	assert min <= x && min <= y; // annotation
	
}
```

#### Precondition
True statements before function is called
```java
method Divide(a: int, b: int) 
  requires b != 0; 
{ // Function body // 
  ... 
}
```

#### Postcondition
Expected behavior after a function is executed. Ensures the function has met its purpose
```java
method Divide(a: int, b: int) returns (result: int)
  requires b != 0;
  ensures result == a / b;
{
  result := a / b;
}

```

#### Invariants
A condition that holds true during the execution of a program or loop

```java
method SumOfArray(arr: array<int>) returns (sum: int)
{
  var i := 0;
  var n := arr.Length;
  var tempSum := 0;

  while i < n
    invariant 0 <= i <= n && sum == tempSum
  {
    tempSum := tempSum + arr[i];
    i := i + 1;
  }

  sum := tempSum;
}
```
# Stronger Condition

- A formula with the property that other formulas is equivalent to it.
```java
method Min(x: int, y: int) returns (min :int)
	ensures min <= x && min <= y
	ensure min == x || min == y // weaker postcondition
{
	if (x < y) {
		min := x; // could also use 'return'
	}
	else {
		min := y; // could also assign to min
	}
}
```

Why strongest post-conditions?
If we can compute them, we can generate `requires` clauses automatically


## Partial Correctness vs Total Correctness

#### Partial
The final state will meeet the postcondition if the program terminates. However, it is not guaranteed the program will terminate

```ocaml
method PartialCorrectnessExample(x: int)
  requires x >= 0;  // Precondition
  ensures x >= 10;  // Postcondition
{
  while (x < 10)
  {
    x := x + 1;
  }
}
```

#### Total
Ensures both postcondition is met and ensures the program terminates
```ocaml
method TotalCorrectnessExample(x: int)
  requires x >= 0;  // Precondition
  ensures x >= 10;  // Postcondition
{
  var i := 0;
  while (i < 10)
  {
    x := x + 1;
    i := i + 1;
  }
}
```


