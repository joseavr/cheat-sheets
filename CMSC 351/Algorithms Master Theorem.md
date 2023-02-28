# Algorithms Master Theorem
Class: [[Algorithms]]
Subject: #
Date: 2023-02-28
Topics: #, #, # 

---

# Master Theorem 

The Master Theorem is a formula for solving recurrence relations that arise in the analysis of algorithms. 

It provides a way to determine the asymptotic complexity of a divide-and-conquer algorithm by looking at its recurrence relation.

The recurrence relation T(n) has the form:

$T(n) = a \cdot T\left( \frac{n}{b} \right) + f(n)$

where
- `a` is the number of subproblems in each recursion 
- `n/b` is the size of each subproblem 
- `f(n)` is the cost of dividing the problem and combining the results.

## How to Solve

- To apply the Master Theorem, we need to
	- compare the function f(n) with $n^{\log_{b}(a)}$
	- where $\log_{b}(a)$ is the logarithm of `a` with base` b`

There are three cases:
1.  If f(n) = $O(n^{\log_{b}(a - ε)})$ for some constant ε > 0, then T(n) = $Θ(n^{\log_{b}(a)})$
2.  If f(n) = $Θ(n^{\log_{b}(a)})$, then T(n) = $Θ(n^{\log_{b}(a)}\cdot \log n)$.
3.  If f(n) = $Ω(n^{\log_{b}(a + ε)})$ for some constant ε > 0 and 
	- if  $a \cdot f\left( \frac{n}{b} \right) ≤ c \cdot f(n)$ for some constant c < 1 and all sufficiently large n, then 
	- $T(n)$ = $Θ(f(n))$

## Example

$T(n) = 2 \cdot T\left( \frac{2n}{3} \right) + 2n -1$

- Here, 
	- a = 2
	- b= 3/2
	- f(n) = 2n - 1
- We can see that
	- $n^{\log_{b}(a)}$ = n ^ $\log_{\frac{3}{2}}(2)$ = n ^ 1.70
- Comparing f(n) with $n^{\log_{b}(a)}$
	- f(n) = 2n - 1 = $Θ(n^{1})$
	- $n^{\log_{b}(a)}$ = $n ^{1.70}$
- Since f(n) = $Θ(n^{\log_{b}(a)})$, we are in case 2 of Master Theorem

- Therefore the solution is:
- T(n) =$Θ(n^{\log_{b}(a)} \cdot log n)$ = $Θ(n ^{1.70} log n)$
- So the Time Complexity of the given recurrence relation is $Θ(n^{1.70} \cdot log n)$


