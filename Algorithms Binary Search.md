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
- 

# Pseudocode
```ruby
Data : Input array A []
Result : Sorted A []

```


# Pseudocode from Class
```ruby

```

## Modified Bubble Sort
```ruby

```


# Binary Search with Counter

```ruby

```