# 🔰 Algorithms QuickSort
Class: <a href="https://github.com/lamula21/cheat-sheets/blob/main/CMSC%20351%20Algorithms/Algorithms.md">Algorithms</a>

Subject: #

Date: 2023-03-09

Topics: #, #, # 

---
# 🎬 Intro to QuickSort
- QuickSort is `in-place`
	- Modifies the input data directly without creating a new one
	- Not need of auxiliarry array to partition
- Quicksort is `not stable`
	- Same elements are inverted because swap at the end
	- e.g [10' , 10*] = [10* , 10']
- QuickSort worst-case solved with `Master Theorem`? **No**
	- Solved with `derivation`

# ⏳ Running Time
- `Worst Case`
	- $Θ(n^{2})$
- `Average Case`
	- $Θ(n \log n)$
- `Best Case`
	- $Θ(n \log n)$

# ⌛ Space Time
- Since `in-place`, quickSort is memory-efficient
- $Θ(1)$


# 🤷🏻‍♂️ What is QuickSort
- QuickSort works by first choosing an element in the list called the pivot value (at some initial pivot index).

- Then rearranging the list (including probably moving the the pivot value) so that 
	- every element smaller than pivot value is to the left of it and 
	- every element larger than the pivot value is to the right of it
- This is called the partitioning process.

- We then apply QuickSort recursively to the left and right sublists.

- **Note**: When QuickSort is applied to a single element it does nothing, since a single element is always sorted.

## Partition Process
- **Pick** an element from the array as a pivot. **Often the last element**
- Pick the leftmost element greater than the pivot value 
	- Swap with the first subsequent element less than or equal to the pivot value.
- Repeating until there are no subsequent elements left. 
- The final swap will be with the first lefmost element and subsequent element (actual pivot value)
- The result will be that 
	- Left part: smaller element $\leq$ pivot value 
	- Right part: larger elements $>$ pivot value

## Example
<img src="https://raw.githubusercontent.com/lamula21/cheat-sheets/main/Assets/20230309111120.png" width="80%" height="80%" />


## Example Partition Handtracing

<img src = "https://raw.githubusercontent.com/lamula21/cheat-sheets/main/Assets/20230315003908.png" width="80%" height="80%"/>

# Pivot Value Choice
- Oftenly choose **last element of array** for pivot
- If chose another element than **last element of array**, we should swap with the last element
	- Or, choose first element as the pivot and modify algorithm (from i=1 to end)

# QuickSort Pseudocode
```java
quickSort( array, start, end )  
	if start < end  
		pivot_index = partition( array, start, end )  
		quickSort( array, start, pivot_index-1 )  
		quickSort( array, pivot_index+1, end )
```

```java
partition( array, start, end )  
	pivot = arr[end], t = start  
	for i = start to end – 1  
		if arr[i] <= pivot  
			swap arr[i] and arr[t]  
			t++  
	swap arr[t] and arr[end]  
	return t
```

- `QuickSort + Partition Best Case`
	- Solved with Master Theorem or derivation
$$T(n) = 2\cdot T\left( \frac{n}{2} \right) + Θ(n)$$
- `QuickSort + Partition Worst Case`
	- Solved only with derivation
$$T(n) = T\left( n-1 \right) + T\left(0\right) + Θ(n)$$


# QuickSort with Counter

```java
quickSort( array, start, end )  
	if start < end  
		pivot_index = partition( array, start, end )  
		quickSort( array, start, pivot_index - 1 )  
		quickSort( array, pivot_index + 1, end )
```

```java
partition( array, start, end )  
	pivot = arr[end], t = start  
	for i = start to end – 1  
		counter++  // Here
		if arr[i] <= pivot  
			swap arr[i] and arr[t]  
			t++  
	swap arr[t] and arr[end]  
	return t
```

# Python Code
```python
def quicksort (a, l ,r):
  if l < r :
    resultingPivotIndex = partition (a,l ,r)
    quicksort (a, l , resultingPivotIndex-1)
    quicksort (a, resultingPivotIndex+1 ,r)
```

```python
def partition (a,l ,r):
  pivotValue = A [ r ]
  t = l
  for i in range (l , r):
    if A [ i ] <= pivotValue:
      temp = A [ t ]
      A [ t ] = A [ i ]
      A [ i ] = temp
      t = t + 1
  temp = A [ t ]
  A [ t ] = A [ r ]
  A [ r ] = temp
  return ( t )
```


# Time Complexity
- QuickSort: $T(k) + T(n − k − 1)$
- Parittion: $c1 + c2(n − 1)$
$$T(n) = T(k) + T(n − k − 1) + c2n + (c1 − c2)$$

## Worst Case
The worst-case occurs when the `partition_pivot_index` is the first or last element in the sublist.

This results in the sublist being only one element smaller than the list itself and the other sublist being length zero. Without loss of generality if k = 0 in the above relation we have
$$T(n) = T(n − 1) + c2n + (c1 − c2)$$
Solving, it results in $T(n) = Θ(n^{2})$.

## Best Case
The best-case occurs when the `partition_pivot_index` is in the middle of the sublist.

This results in the sublists being of equal size. Then in the above relation we have 
$$T(n) = 2T(n/2) + c2n + (c1 − c2)$$
which results in $T(n) = Θ(n \cdot lg n$) by the Master Theorem