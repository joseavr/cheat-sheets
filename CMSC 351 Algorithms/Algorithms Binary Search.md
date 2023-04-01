# 🔰 Algorithms Binary Search

📚Class: CMSC 351 Algorithms

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/CMSC%20351%20Algorithms/Algorithms.md">Algorithms</a>

✏️Section: 0301

🗓️Date: 2023-02-13

---

# 🎬 What is Binary Search 
- Given a sorted list of elements and a target element, 
	- Finds the index of the target element or 
	- Returns failure if the target element does not exist.

# ⏳ Running Time
- `Worst Case`
	- $\theta(\log n)$
- `Best Case`
	- $\theta(1)$
- `Average Case`
	- $\theta(\log n)$


# 🤷🏻‍♂️ How It Works
- The algorithm first looks at the middle of the list. 
	- If if element is not there then it knows by comparison if the element is on the left or the right side of that middle element. 
	- Search that half of the list and repeats. 
- It keeps repeating this process either until 
	- it finds the element 
	- or until list shrinks to length 1 and the element is not found.

## Example

Consider the list with 20 elements. We wish to find the number 17. 
$$A = [0,0,4,4,6,7,8,9,9,10,12,13,13,14,14,17,18,19,19,19]$$
`Iteration 1`
- Set Start and End indixes
	- S = 0
	- E = 19 (`E = len(A) - 1`)
- Find the center index
	- C = ⌊(19+0)/2⌋ = 9
	- A[9]=10
- Compare 
	- A[9] == 17? Nope
	- 10 < 17
	- 17 is greater, so 17 must be on the right
	- Search the second half (right half)

`Repeat Iteration until found element`
- Set Start and End indices
	- S = C + 1 = 10
	- E = 19
- Find the center
	- C = ⌊(19+10)/2⌋ = 14
	- A[14] = 14
- Compare
	- A[14] == 17? Nope
	- 14 < 17
	- 17 is greater, so 17 must be on the right
	- Search the second half

`Final iteration`

| INDEX | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  | 11  | 12  | 13  | 14  | 15  | 16  | 17  | 18  | 19  |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARRAY | 0   | 0   | 4   | 4   | 6   | 7   | 8   | 9   | 9   | 10  | 12  | 13  | 13  | 14  | 14  | 17  | 18  | 19  | 19  | 19  |

- Set Start and End indices
	- S = C + 1 = 15
	- E = 16
- Find the center
	- C = ⌊(16 + 15)/2⌋ = 15
	- A[15] = 17
- Compare
	- A[15] == 17? Yep
	- 17 = 17
	- We found it! So, we return the index 15.


# Pseudocode
```python
Data : Input array A []
Result : Sorted A []

function binarysearch(A,TARGET)
	# c1
	L=0  
	R=len(n)-1 

	# ?? iterations
	while L <= R
		# c2 
	    C = floor((L+R)/2)
	    if A[C] == TARGET
			return C
		elif TARGET < A[C]
		    R = C-1
		elif TARGET > A[C]
		    L = C+1
		    
    return FAIL # c3
```

# Time Complexity
- `Worst Case`
The worst-case scenario happens if **TARGET** is never found.

Initially, length n.

After the first iteration the sublist length is $\frac{n}{2}$ .

After the second iteration the sublist length is $\frac{n}{4}$ .

This continues such that after k iterations the sublist length is $\frac{n}{2^k}$.

Worst case scenario, the while loop iterates until L=R and then at the end of that iteration $R<L$ and it fails. We have L=R when the sublist length is 1:
$$\frac{n}{2^k} = 1$$
$$2^{k} = n$$
$$k = \log n$$

It has one more iteration when $L==R$, then it iterates $(1 + lgn)$ times and then the condition fails.

It follows that the total time requirement is:  
$$T(n)=c1 +c2(1+lgn)+c3$$
$$T(n_) = Θ(lgn)$$

- `Base Case`
If the target is immediately located at C=floor((L+R)/2) at the start of the first iteration then the total time requirement is:
$$T (n) = c1 + c2 = Θ(1)$$