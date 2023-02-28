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
- `a` is the number of subproblems in each recursions, $a \geq 1$
- `n/b` is the size of each subproblem, $b > 1$
- `f(n)` is the cost of dividing the problem and combining the results.
	- f(n) = $Θ (n^{k} \cdot \log^{p}(n))$

## Cases
- Compare the function `f(n)` from $T(n)$ with  $Θ (n^{k} \cdot \log^{p}(n))$
- We would need to find two values
	- $\log_{b}(a)$
	- $k$
- Based on these 2 values, there are three cases:
	1. If $\log_{b}(a)$ > $k$ => $Θ(n^{\log_{b}(a)})$

	2. If $\log_{b}(a)$ = $k$
		- If $p > -1$ =>   $Θ(n^{k} \cdot \log^{p+1}n)$
		- If $p = -1$ =>  $Θ(n^{k} \cdot \log(\log n))$
		- If $p < -1$ =>  $Θ(n^{k})$

	3. If $\log_{b}(a)$ < $k$  
		- If $p >= 0$   =>   $Θ(n^{k} \cdot \log^{p}n)$
		- If $p < 0$   =>  $O(n^{k})$


## How to Solve
- Given $T(n) = a \cdot T\left( \frac{n}{b} \right) + f(n)$
	- Find `a`
	- Find `b`
	- Find `f(n)`

- Compare the function `f(n)` with  $Θ (n^{k} \cdot \log^{p}(n))$
	- FInd `k`
	- Find `p`
	- Find $\log_{b}(a)$
- FInd `Case#` by comparing $\log_{b}(a)$ with `k`
- Get answer. Done

## Example Case 1

Let T(n) = 2 T(n/2) + 1
- a = 2
- b = 2
- f(n) = $Θ(1)$ 
	- f(n) = $Θ(n^{0} \log^{0}n)$
	- Compare $Θ(n^{0} \log^{0}n)$ = $Θ(n^{k} \cdot \log^{p}n)$
- Find `k` and `p` and $\log_{b}(a)$
	- k = 0
	- p = 0 
	- $\log_{b}(a)$ = $\log_{2}(2)$ = 1
 - $\log_{2}(2)$ > k
	 - 1 > 0
- The answer 
	- $Θ(n^{\log_{b}a})$ = $Θ(n^{\log_{2}2})$ = $Θ(n^{1})$

## IGNORE THIS

1. If f(n) = $O(n^{\log_{b}(a - ε)})$ for some constant ε > 0, then T(n) = $Θ(n^{\log_{b}(a)})$
2.  If f(n) = $Θ(n^{\log_{b}(a)})$, then T(n) = $Θ(n^{\log_{b}(a)}\cdot \log n)$.
3.  If f(n) = $Ω(n^{\log_{b}(a + ε)})$ for some constant ε > 0 and 
	- if  $a \cdot f\left( \frac{n}{b} \right) ≤ c \cdot f(n)$ for some constant c < 1 and all sufficiently large n, then 
	- $T(n)$ = $Θ(f(n))$


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


