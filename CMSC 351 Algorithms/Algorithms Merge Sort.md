# 🔰 Algorithms Merge Sort
Class: <a href="https://github.com/lamula21/cheat-sheets/blob/main/CMSC%20351%20Algorithms/Algorithms.md">Algorithms</a>
Subject: #
Date: 2023-02-28
Topics: #, #, # 

---
# ⏳ Running Time
Same time complexity since MergeSort breaks down the list and puts it back together no matter what, even if the list is sorted at the start. 

- `Worst Case`
	- $\theta(n \log n)$
- `Average Case`
	- $\theta(n \log n)$
- `Best Case`
	- $\theta(n \log n)$

# ⌛️ Space Time
MergeSort creates sub-lists
- $\theta(n)$

# 🤷🏻‍♂️ What is Merge Sort
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



# Pseudocode