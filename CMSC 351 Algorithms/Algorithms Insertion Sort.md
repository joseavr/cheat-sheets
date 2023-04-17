# 🔰 Algorithm Insertion Sort

📚Class: CMSC 351 Algorithms

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/CMSC%20351%20Algorithms/Algorithms.md">Algorithms</a>

✏️Section: 0301

🗓️Date: {{date}}

---

# 🎬 Intro to Insertion Sort 
- Insertion Sort is `in-place`
	- Not need of an auxiliarry array
- Insertion Sort is `stable`
	- Same elements won't be swapped since it only swaps if an element is less than the other
	- if a < b , then swap

# ⏳ Runtime
- `Worst Case`
	- $Θ(n^2)$
- `Best Case`
	- $Θ(n)$
- `Average Case`
	- $Θ(n^2)$

# ⌛️ Space Time
- $Θ(1)$


# 🤷🏻‍♂️ How It Works
- Take array `A[ ] = [7,4,5,2]`
![](../Assets/20230221002736.png)

- Example 2:
![](../Assets/20230221003527.png)


# Pseudocode
```python
func insertionSort(A)
	n = len(A)
	for i=1 to n-1 do
	    j=i
	    while j>0 and A[j-1] > A[j] do
			swap(A[j], A[j-1])
	        j = j-1
	    end
	end
end 
```


