# 🔰 Algorithms Rigorous Time
Class: <a href="https://github.com/lamula21/cheat-sheets/blob/main/CMSC%20351%20Algorithms/Algorithms.md">Algorithms</a>
Subject: #
Date: 2023-02-28
Topics: #, #, # 

---


## Sequential Search Running time
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

Statement | Running time

(1) | 1 + (between 1 and (n+1)) + (between 0 and n)

(2) | n

(3) | 1

(4) | 1

Taking the lower and upper bounds

1 + (1) + (0) + 1 + 1 <= T(n) <= 1 + (n+1) + n + n + 1

# Simple Statements Running Time
- when computing big theta, we dont care about multiplying constants.

    - int a = 0
    - int b 

# Loop Running Times
- for loop, while loop, do-while loop, = Theta(n)

# Conditionals Running Times
- if, if-else, switch = Theta(1)
- If a for-loop inside of if-statement, then the runnnig time is Theta(n)
  
```java
if (a < b) {
    for i = 0 to n-1
        output i
}
```
- `Big theta` of the above code is Theta(n)
- Average case: 50% of the time, a < b, 
  - 50% of the time a>= b