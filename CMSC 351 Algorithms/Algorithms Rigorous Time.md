# 🔰 Algorithms Rigorous Time

📚Class: CMSC 351 Algorithms

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/CMSC%20351%20Algorithms/Algorithms.md">Algorithms</a>

✏️Section: 0301

🗓️Date: 2023-01-30

---

# Statements Time
- Statements takes time

They are constants:
- a=0 → $c_{1}$
- b=0 → $c_{2}$
- c=0 → $c_{3}$

These statements takes the same amount of time (whether true or false), but for time complexity doesn't matter. It is a just a constant:
- a=0 
- b=0   → $c_{1}$
- c=0 
- Therefore $c_{1}$ = $Θ(1)$


# For Loops Time

Assume iterating a list of `n` size:
```python

sum = 0    # c1
for i = 1 to n    # c2 in n times
    // Comment    # c3 in n times
end
```

- **Total time cost**: 
	- $c_{1} + c_{2} n + c_{3} n = Θ(n)$

However, since constants are dropped, most programmers just loop on the time taken by the loop to find the time complexity:
```python
sum = 0    # c1
for i = 1 to n    # (n-i+1) = iterates n times
    // Comment    # c3 in n times  <- we take this for Time Complexity
end
```
- **Total time cost**: 
	- $c_{3} n =  Θ(n)$


# While Loops Time
```python
sum = 1 # c1
i=1 # c2
while i <= n  # c3 in n times 
    i=i+1     # c4 in n times
end
```
- **Total time cost**: 
	- $c_{1} + c_{2} + c_{3} n + c_{4} n = Θ(n)$

**Faster way**:
```python
sum = 1 # meh
i=1 # meh
while i <= n  # iterates n times 
    i=i+1     # c1 in n times
end
```
- **Total time cost**: 
	- $c_{1} n = Θ(n)$

# Conditionals Time
- if, if-else, switch = $Θ(1)$
- If a for-loop inside of if-statement = Θ(n)

```python
if a<b           # c1 
    print(’hi’)  # c2
end
```
- If a<b passes then the time is c1 + c2.
- If a<b fails then the total time is c1.

Often then we’ll just say the whole thing is constant time:
```python
if a<b
    print(’hi’)     -> c1
end
```
- **Total time cost**:
	- $c_{1} = Θ(1)$

*Note*: it is constant depending on what is in the body of the conditional
- Like if we have a for loop, then the constant time of the if statement changes

# Combining
```python
if a<b  # c1 
    sum = 0 # c2
    for i = 1 to n # c3 in n times
        sum = sum + i # c4 in n times
```

Formally the conditional check $c_{1}$ time no matter what. But then observe:
- If a<b passes then the total time is $c1+c2+c3n+c4n=Θ(n)$
- If a<b fails then the total time is $c1 = Θ(1)$ (formally is 0, but since normally we have code before this if-statement, the time is constant $Θ(1)$)

# Best Case - Worst Case
```python
print(’hi’) # c5
if a<b  # c1 
    sum = 0 # c2
    for i = 1 to n # c3 in n times
        sum = sum + i # c4 in n times
```

Many resources (all over the internet) would simply say that this is O(n) but the truth is a bit more nuanced. The reality is:
- In a best-case scenario a<b fails and the time is c5 + c1 which is in fact Θ(1). It’s also O(1) and Ω(1). Of course it is also O(n) but this is being pretty liberal.
    
- In a worst-case scenario a<b passes and the time is c5 + c1 + c2 + c3n + c4n which is in fact Θ(n). It’s also O(n) and Ω(n).
    
- If anyone says casually that this is O(n) what they mean is that in the worst case it is O(n).
- Average case: 
	- 50% of the time, a < b, 
	- 50% of the time a>= b

# Time Analysis
So how far can we actually simplify if we’re interested only in time complexity? In other words, what do we need to keep?

## 1️⃣ Example
In this example:  
- c1 iterates $n^{2}$ times
- c2 iterates $n^{2}$ times
```python
for i=n to n^2 # c2 iterates n^2 times
	print(i)   # c2 iterates n^2 times
```

We can ignore the c1:
```python
for i=n to n^2
	print(i)   # c2 iterates n^2 times
```

The (best, worst, and average) time complexity is $Θ(n^{2})$:   
- Any line that takes constant time can be ignored provided there is other adjacent code which takes nonzero time.

## 2️⃣ Example Worst Case
```python
if a+b<c                # c1
    for i = 1 to n      # c2 in n times
        print(’spicy’)  # c3 in n times
```

For worst-case time complexity we can ignore the c1 and c2:
- The worst-case time complexity is c3*n = Θ(n)

## 3️⃣ Example Best Case

```python
if a+b<c                # c1
    for i = 1 to n      # c2 in n times
        print(’spicy’)  # c3 in n times
```

For best-case time complexity if a+b<c fails then we cannot ignore the c1 (because a+b<c is run one time) but we can ignore everythign else:
```python
if a+b<c                # c1
    for i = 1 to n      
        print(’spicy’)
```
- The best-case time complexity is c1 = Θ(1).


# Sequential Search Running time
- This algorithm searches an array of N elements for a given target value.
- The running time of the sequential search algorithm is proportional to the length of the array.
  
```java
public static int sequentialSearch(int[] data, int target) { 
    for (int i = 0; i < data.length; i++) { // (1)
        if (data[i] == target) {    // (2)
            return i;   // (3)
        }
    }
    return -1;  // (4)
}
```

Statement | Running time:
(1) | 1 + (between 1 and (n+1)) + (between 0 and n)

(2) | n

(3) | 1

(4) | 1

Taking the lower and upper bounds:
1 + (1) + (0) + 1 + 1 <= T(n) <= 1 + (n+1) + n + n + 1
