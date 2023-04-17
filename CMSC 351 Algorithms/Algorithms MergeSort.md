# 🔰 Algorithms MergeSort

📚Class: CMSC 351 Algorithms

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/CMSC%20351%20Algorithms/Algorithms.md">Algorithms</a>

✏️Section: 0301

🗓️Date: {{date}}

---
# 🎬 Intro to MergeSort
- MergeSort is `not in-place`
	- Needs of an auxiliary array to sort
- MergeSort is `stable`
	- Meaning, two same elements will not be inverted
	- [10';10*] -> After mergeSort -> [10';10*] 
- MergeSort worst-case solved with `Master Theorem`? **Yes**
- MergeSort recurrence relation:
$$T(n) = 2\cdot T(\frac{n}{2}) + f(n)$$
# ⏳ Running Time
Same time complexity since MergeSort breaks down the list and puts it back together no matter what, even if the list is sorted at the start. 

- `Worst Case`
	- $Θ(n \log n)$
- `Best Case`
	- $Θ(n \log n)$
- `Average Case`
	- $Θ(n \log n)$

# ⌛️ Space Time
- Since MergeSort creates sub-lists (`not in-place`)
- $Θ(n)$

# 🤷🏻‍♂️ What is MergeSort
- Merge sort is a divide-and-conquer algorithm 
	- the list is subdivided repeatedly in half. 
	- Each half is then divided in half again and so on until each sublist has size 1 and is obviously sorted. 
	- Pairs of sublists are then merged to preserve the sort.

- Here is a visual representation. 
	- The red/blue divided (sub)list in half. 
	- Green are sorted. 
	- Action above the center is the recursive deconstruction while 
	- Action below the center is the re-merging of the sublists.

<img src="https://raw.githubusercontent.com/lamula21/cheat-sheets/main/Assets/20230315135410.png" width="60%" height="60%">

- `Note`:
	- Sorting does not happen in parallel but **SEQUENTIALLY**
	- e.g, Left half of the array gets sorted first then right half

# Pseudocode
- If the array has only one element (or empty), already sorted, thus do nothing, otherwise
	- MergeSort left half of array
	- MergeSort right half of array
	- Merge two sorted half-arrays into one sorted array
```python
mergeSort(A , start , end )
	if start < end
		m = len(A) // 2   # middle-element of A index
		left_A = mergeSort(A , s , m-1 )
		righ_A = mergeSort(A , m , end)
		return merge(left_A , right_A)
	else # empty or 1 element array
		exit
```

```python
merge(L , R)
	C = []
	while len(L) > 0 && len(R) > 0
		if L.head <= R.head
			C.append( L.head )
			L.shift() # remove head
		else
			C.append( R.head )
			R.shift() # remove head

	while len(L) > 0
		C.append( L.head )
		L.shift() # remove head
	
	while len(R) > 0
		C.append( R.head )
		R.shift() # remove head

	return C
```

- `MergeSort + Merge Recurrence`
$$T(n) = T\left( \frac{n}{2} \right) + T\left(\frac{n}{2}\right) + Θ(n)$$
- `MergeSort + Merge Best Case`
$$T(n) = 2\cdot T\left( \frac{n}{2} \right) + \frac{n}{2}$$
- `MergeSort + Merge Worst Case`
$$T(n) = 2 \cdot T\left(\frac{n}{2}\right) + n-1$$
