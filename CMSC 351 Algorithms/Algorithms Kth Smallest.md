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

## 1️⃣ Sorting First
- Could sort first the list and then find the $(k-1)$ index to find the kth smallest
- Could use MergeSort or HeapSort: 
	- $Θ(nlgn)$


## 2️⃣ Partial Sorting
- Run a partial Selection Sort or a partial Bubble Sort (reversed Bubble Sort, filling in the min values first)
- Each pass of reverse Bubble sort will fix one more starting element and so if we do k passes the time will essentially be:

$$n + (n − 1) + (n − 2) + ... + (n − k − 1) = Θ(kn) $$

- If k is $\frac{n}{4}$ or $\frac{n}{2}$ or $\frac{3n}{4}$ then
	- $Θ( n^{2})$
- If k is small (1 or 2) then
	- $Θ( n )$
- Not really better than brute force approach.


## 3️⃣ Min Heap
- We could build a **min heap**. When we built a max heap we said it was worse-case O(n lg n) time complexity but this is not asymptotically tight and in fact it is worse-case O(n) (we have not shown this) and the same is true for a min heap. Since extracting an element and fixing the heap takes worst-case O(lg n) time and we would do this k times the time complexity would be worse-case O(n + k lg n).

These are all pretty good and interesting but can we do better overall? Perhaps something that’s O(n) no matter what k is?


# ✏️ Quicksort The Best

## MOM Method
Now on to how the Median of Medians method actually will work. 

Let's say we want to perform MOM-x on a list of $n$ elements:
- Divide the list into ⌊n/x⌋ sublists of length $x$ , sort those sublists.
- Select the median of each sublist. For the final sublist if it has two or four elements select the lower median.
- Apply **selectkth** recursively on the smaller list of those values in order to find the median (or lower median) of that new list.


## Example
Demonstrate MOM-5 on the following list of 15 elements: 
$$60,36,73,50,44,90,17,38,61,45,9,22,85,33,100$$

`Step 1`: Divide the list into sublist of size 5
$$60,36,73,50,44\mid90,17,38,61,45\mid9,22,85,33,100$$

Since we have $\left \lceil{\frac{15}{5}}\right \rceil = 3$ sublists, thus 3 columns

| 1st column | 2nd column | 3rd column |
| ---------- | ---------- | ---------- |
| 60         | 90         | 9          |
| 36         | 17         | 22         |
| 73         | 38         | 85         |
| 50         | 61         | 33         |
| 44         | 45         | 100        |


`Step 2:` Sort each sublist (columns)

| 1st column | 2nd column | 3rd column |
| ---------- | ---------- | ---------- |
| 36         | 17         | 9          |
| 44         | 38         | 22         |
| 50         | 45         | 33         |
| 60         | 661        | 81         |
| 73         | 90         | 100        |

`Step 3`: Pick the median of medians
- The median of 1st column: 50
- The median of 2nd column: 45
- The median of 3rd column: 33
- The median of {33,45,50}: 45
- **Note**: if the set of medians is even, select the lower median

Thus the value of MOM-5 = 45

`Step 4:` Find elements **GUARANTED** smaller/greater
We can notice that values **GUARANTED** to be smaller than MOM=45:
- Elements above of 45: {38, 17}
- Next column less than 45: {33, 22, 8}
- So elements **GUARANTED** smaller than 45 is {8, 17, 22, 33, 38}

We can also notice values **GUARANTED** to be greater than MOM=45:
- Elements belove of 45: {661, 90}
- Next column greater than 45: {50, 60, 73}
- Elements **GUARANTED** greater than 45 is {50, 60, 73, 90, 661}

## Formulas

1. Number of elements in the list less than MOM-x
	- Number of columns guaranted: $\left\lceil \frac{n/x}{2}\right\rceil$
	- Number of rows guaranted: $\left\lceil \frac{x}{2}\right\rceil$
	- Thus, $\#columns \cdot \#rows -1(without MOM)$  
2. Same for number of elements in the list greater than MOM-x


## Pesudocode
```python
def selectkth(A,L,R,k) 
    momindex = mom(A[L:R]) 
    swap( A[momindex] , A[R] )
    pivotindex = partition(A,L,R)
    
    if k-1 < pivotindex
        return(selectkth(A,L,pivotindex-1,k)) 
    else if k-1 > pivotindex
        return(selectkth(A,pivotindex+1,R,k)) 
    else
        return(A[pivotindex])


def partition(A,L,R) 
    same as quicksort

def mom(A,L,R)  
    divide A into sublists and sort those  
    mlist = new list of (lower?) medians of sublists  
    s = apply selectkth to get the (lower?) median of mlist 
    return index
```


