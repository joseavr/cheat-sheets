# Algorithms QuickSort
Class: [[Algorithms]]
Subject: #
Date: 2023-03-09
Topics: #, #, # 

---

# Intro to QuickSort

# Running Time
- `Worst Case`
	- $\theta(n^{2})$
- `Average Case`
	- $\theta(n \log n)$
- `Best Case`
	- $\theta(n \log n)$

# Space Time
- $\theta(1)$


# What is QuickSort
- QuickSort works by first choosing an element in the list called the pivot value (at some initial pivot index).

- Then rearranging the list (including probably moving the the pivot value) so that 
	- every element smaller than pivot value is to the left of it and 
	- every element larger than the pivot value is to the right of it
- This is called the partitioning process.

- We then apply QuickSort recursively to the left and right sublists.

- **Note**: When QuickSort is applied to a single element it does nothing, since a single element is always sorted.

## Partition Process
- **Pick** an element from the array as a pivot
- Pick the leftmost element which is greater than the pivot value and swap it with the first subsequent element which is less than or equal to the pivot value.
- Repeating until there are no subsequent elements left. 
- The final swap will be with the actual pivot value and the result will be that 
	- Left part: smaller element $\leq$ pivot value 
	- Right part: larger elements $>$ pivot value

## Example
![](../Assets/20230309111120.png)


## Example 2

![[20230309112757.png]]

# Pivot Value Choice


# QuickSort Pseudocode
```java
quickSort( array, start, end )  
	if start < end  
		index = partition( array, start, end )  
		quickSort( array, start, index - 1 )  
		quickSort( array, index + 1, end )
```


# Partition Process Pseudocode

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

# QuickSort with Counter

```java
quickSort( array, start, end )  
	if start < end  
		partition_pivot_index = partition( array, start, end )  
		quickSort( array, start, index - 1 )  
		quickSort( array, index + 1, end )
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