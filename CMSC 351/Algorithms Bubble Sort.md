# Bubble Sort
Class: [[]]
Subject: #
Date: 2023-02-09
Topics: #, #, # 

---

# What is Bubble Sort 

- Loops through each element of an array and checks
```ruby
if current_element > next_element then 
	swap current_element and next_element
```

![[Pasted image 20230209111836.png]]

- Memory space needed $\theta(1)$
	- Needs two variables to store i and j, two indexes
	- an extra variable when we swap elements, temp
- Stable sorting algorithm
	- if two elements are the same, they remain the same
# Pseudocode
```ruby
Data : Input array A []
Result : Sorted A []

int i , j ; 
N = length ( A ) ; 
for j=0 to N-1 do
	for i=0 to N-1 do
		if A [i] > A [i +1] then
			temp = A [i]; # temp big number , A[i+1] small number
			A [i] = A [i+1]; # Place small number to current position
			A [i+ 1] = temp ; # Place big number to the next position 
		endif
	endfor
endfor
```

# Running Time
- No matter what, running time: $\theta (n^2)$
$$
T( n ) = ( n – 1 ) + ( n – 2 ) + ... + 2 + 1
$$
$$
T( n ) = ( n – 1 ) * \frac{n}{2} = Θ( n^2 )
$$
## Worst Case
- 
## Average Case

## Best Case
- $\theta(n)$

# Pseudocode from Class
```ruby
For i = 0 to n – 2, increasing by 1 each time  
	For each j from 0 to n - 2 - i, increasing by 1 each time  
		If value at index j is greater than value at index j +1  
		Swap value at index j with value at index j + 1
```
## Modified Bubble Sort
```ruby
swapped = true  
For i = 0 to n – 2, increasing by 1 each time AND swapped == true  
	swapped = false  
	For each j from 0 to n - 2 - i, increasing by 1 each time  
		If value at index j is greater than value at index j +1  
			Swap value at index j with value at index j + 1  
			swapped = true
```
## Running Time
- Worst Case, Average Case, running time remains $\theta(n^2)$
- Only one pass (no swap is detected) => $\theta(n)$


# Bubble Sort with Counter

```ruby
For i = 0 to n – 2, increasing by 1 each time  
	For each j from 0 to n - 2 - i, increasing by 1 each time  
		Counter++  
		If value at index j is greater than value at index j +1  
			Swap value at index j with value at index j + 1
```