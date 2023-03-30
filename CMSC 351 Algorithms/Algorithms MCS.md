# 🔰 Algorithms Maximum Contiguous Sum

📚Class: CMSC 351 Algorithms

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/CMSC%20351%20Algorithms/Algorithms.md">Algorithms</a>

✏️Section: 0301

🗓️Date: {{date}}

---

# Maximum Contiguous Sum (MCS) problem
- we have a list of integers: $[-9, 3, 1, 1, 4, -2, -8]$
- There are many contiguous sub-lists: $[3,1,1] , [1,1], [4], [4,-2], [-2,-8], ...$
- The sub list $[3,4]$ is NOT a contiguous sub-list
- What is the maximum sum for all the possibe contiguous sub-lists?
  
## Brute Force Solution
- Usually not good idea

```java
max = list[0]
for i=0 to n-1
    for j=i to n-1
        calculate sum of sub-list between indexes i and j
        update max as appropriate
```

```java
max = list[0]
for i=0 to n-1
    for j=i to n-1
        sum = 0
        for k=i to j
            sum += list[k]
        if sum > max
            max = sum
```

Another brute force solution
- T = n (n+!)/2 = Theta(n^2)

```java
max = list[0]
for i=0 to n-1  // starting index
    sum = 0
    for j=i to n-1  // ending index (must be >= i)
        sum += list[j]
        if sum > max
            max = sum
```
