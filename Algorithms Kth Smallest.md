# 🔰 Algorithms Kth Smalletst

📚Class: CMSC 351 Algorithms

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/CMSC%20351%20Algorithms/Algorithms.md">Algorithms</a>

✏️Section: 0301

🗓️Date: 2023-03-30

---

# 🤷🏻‍♂️ What is Kth Smallest
- **Problem**: 
	- We have a list of $n$ distinct numbers (NOT ordered)  
	- Find the $k^{th}$ smallest number in the list
- Useful for finding the minimum, the maximum, and, what is valuable to us, the median.

- Example:
	- { 45, 23, 16, 87, 90, 19, 6 }  
	- 2nd smallest is 16  
	- 4th smallest is 23

# ✏️ Brute-Force Method
- Finding the $k^{th}$ order entry might be to first find the smallest, then the next smallest, and so on, until we reach the $k^{th}$ smallest.
- **Idea**: 
	- Find the minimum and assign it to kth. 
	- Iterate by repeatedly: 
		- Go through A and 
		- Find the smallest which is less than the maximum but larger than $k^{th}$.
	- This would be the next smallest. 
	- We do this k-1 times
- The kth order element in a list is the kth smallest entry
	- The $1^{th}$ order element: 1st minimum entry.
	- The $2^{th}$ order element: 2nd minimum entry.
	- so on

## Pseudocode
```python
def kthOrder (A , k ):
	n = length of A  
	mini = minimum element in A  
	maxi = maximum element in A  
	kth = mini  

	for i=1 to k-1
		nextsmallest = maxi 		
		# Loop through all the elements of A and update
		for j=0 to n-1:
			# nextSmallest as appropriate 
			if (A[j] < nextsmallest) and (A[j] > kth) 
				nextsmallest = A[j]
			# update kth: kth = nextSmallest
			kth = nextsmallest
	return kth # => int
```

## ⏳ Time Complexity
- Finding the maximum and minimum is Θ(n). 
- The inner loop is Θ(n) and iterates k − 1 times, 
	- $Θ(n(k − 1))$
- The entire algorithm:
	- $Θ(n + n(k − 1)) = Θ(kn)$

# 🙋‍♂️ Could We possibly Do Better?
Yes, there are a number of other approaches including:

## Sorting First
- Could sort first the list and then find the $(k-1)$ index to find the kth smallest
- Could use MergeSort or HeapSort: 
	- $Θ(nlgn)$


## Partial Sorting
- Run a partial Selection Sort or a partial Bubble Sort (reversed Bubble Sort, filling in the min values first)
- Each pass of reverse Bubble sort will fix one more starting element and so if we do k passes the time will essentially be:

$$n + (n − 1) + (n − 2) + ... + (n − k − 1) = Θ(kn) $$

- If k is $\frac{n}{4}$ or $\frac{n}{2}$ or $\frac{3n}{4}$ then
	- $Θ( n^{2})$
- If k is small (1 or 2) then
	- $Θ( n )$
- Not really better than brute force approach.


## Min Heap
- We could build a **min heap**. When we built a max heap we said it was worse-case O(n lg n) time complexity but this is not asymptotically tight and in fact it is worse-case O(n) (we have not shown this) and the same is true for a min heap. Since extracting an element and fixing the heap takes worst-case O(lg n) time and we would do this k times the time complexity would be worse-case O(n + k lg n).

These are all pretty good and interesting but can we do better overall? Perhaps something that’s O(n) no matter what k is?


# Quicksort 
## MOM Method