# 🔰 Algorithms Master Theorem

📚Class: CMSC 351 Algorithms

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/CMSC%20351%20Algorithms/Algorithms.md">Algorithms</a>

✏️Section: 0301

🗓️Date: {{date}}

---

# 🎬 Master Theorem 

The Master Theorem is a formula for solving recurrence relations that arise in the analysis of algorithms. 

It provides a way to determine the asymptotic complexity of a divide-and-conquer algorithm by looking at its recurrence relation.

The recurrence relation T(n) has the form:

$$T(n) = a \cdot T\left( \frac{n}{b} \right) + f(n)$$
where
- `a` is the number of subproblems in each recursions, $a \geq 1$
- `n/b` is the size of each subproblem, $b > 1$
- `f(n)` is the cost of dividing the problem and combining the results.
	- $f(n)$ = $Θ (n^{c} \cdot \log^{P}(n))$

## Cases
- Compare the function `f(n)` from $T(n)$  with  $Θ (n^{c} \cdot \log^{P}(n))$
- We would need to find two values
	- $\log_{b}(a)$
	- $c$
	- Find $c$ by doing $Θ$ of `f(n)`

- Based on these 2 values, there are 3 cases:
	- `Case 1`: If $f(n)$ = $O(n^{c})$ AND $\log_{b}(a)$ > $c$   
		- $\longrightarrow$ $T(n) = Θ(n^{\log_{b}(a)})$

	- `Case 2`: If $f(n)$ = $Θ(n^{c})$ AND $\log_{b}(a)$ = $c$
		- $\longrightarrow$ $T(n) = Θ(n^{c} \cdot \log n)$
		- Extra cases:
		- If $p > -1$  $\longrightarrow$   $Θ(n^{c} \cdot \log^{P+1}n)$
		- If $p = -1$  $\longrightarrow$  $Θ(n^{c} \cdot \log(\log n))$
		- If $p < -1$  $\longrightarrow$  $Θ(n^{c})$

	- `Case 3`: If $f(n) = Ω(n^{c})$ AND $\log_{b}(a)$ < $c$  
		- $\longrightarrow$ $T(n) = Θ(f(n))$
		- Extra cases:
		- If $p >= 0$   $\longrightarrow$   $Θ(n^{c} \cdot \log^{p}n)$
		- If $p < 0$      $\longrightarrow$  $O(n^{c})$
		- **Note**: For this, case, $f(n)$ must satisfy `regularity condition`:
			- There is some $C < 1$ and $n_{0}$ such that $a \cdot f( \frac{n}{b}) \leq C \cdot f(n)$

## How to Solve
- `Step 1`: Given $T(n) = a \cdot T\left( \frac{n}{b} \right) + f(n)$
	- Find `a`
	- Find `b`
	- Find `f(n)`

- `Step 2`: Get $Θ$ of the function `f(n)` and compare with  $Θ (n^{c} \cdot \log^{p}(n))$
	- FInd `c`
	- Find `p`
	- Find $\log_{b}(a)$
- `Step 3`: Find `Case#` by comparing $\log_{b}(a)$ with `c`
- `Step 4`: Get answer. Done

## Example Case 1
$T(n) = a \cdot T\left( \frac{n}{b} \right) + f(n)$
- Given $T(n) = 8 \cdot T\left( \frac{n}{2} \right) + n^{2} - n$
- **Observation 1**: $f(n) = n^{2} - n$ = $Θ(n^{c})$ with `c = 2`
- **Observation 2**: $\log_{b}a$ = $\log_{2}8$ = 3, so $\log_{b}a > c$ 
- **Summary**: $f(n) = O(n^{c})$ and $c < \log_{b}a$ Hence `Case 1` 
- **Conclusion**: $T(n) = Θ(n^{\log_{b}a})$ =  $Θ(n^{\log_{2}8})$ = $Θ(n^{3})$


## Example Case 2
$T(n) = a \cdot T\left( \frac{n}{b} \right) + f(n)$
- Given $T(n) = 8 \cdot T\left( \frac{n}{2} \right) + n^{3} + n$
- **Observation 1**: $f(n) = n^{3} + n$ = $Θ(n^{c})$ with `c = 3`
- **Observation 2**: $\log_{b}a$ = $\log_{2}8$ = 3, so $\log_{b}a = c$ 
- **Summary**: $f(n) = Θ(n^{c})$ and $c = \log_{b}a$ Hence `Case 2` 
- **Conclusion**: $T(n) = Θ(n^{\log_{b}a} \log n)$ =  $Θ(n^{\log_{2}8} \log n)$ = $Θ(n^{3} \log n)$

## Example Case 3
$T(n) = a \cdot T\left( \frac{n}{b} \right) + f(n)$
- Given $T(n) = 8 \cdot T\left( \frac{n}{2} \right) + n^{4} + n$
- **Observation 1**: $f(n) = n^{4} + n$ = $Θ(n^{c})$ with `c = 4`
- **Observation 2**: $\log_{b}a$ = $\log_{2}8$ = 3, so $\log_{b}a < c$ 
- **Summary**: $f(n) = Ω(n^{c})$ and $c > \log_{b}a$ Hence `Case 3` 
- **Conclusion**: $T(n) = Θ(f(n))$ =  $Θ(n^{4} + n)$ = $Θ(n^{4})$
- **Note**:  $f(n) = n^{4} + n$ must satisfy `regularity condition`:
	- $a \cdot f( \frac{n}{b}) \leq C \cdot f(n)$
	- $a \cdot f\left( \frac{n}{2} \right) = 8\cdot (( \frac{n}{2} )^{2} + (\frac{n}{2}))$ = $\frac{1}{2} (n^{4} + 4n)$
	- $\frac{3}{4} f(n)$ = $\frac{3}{4} (n^{4} + n)$
	- Comparing Leading Coefficients
		- $\frac{1}{2} (n^{4} + 4n) < \frac{3}{4} (n^{4} + n)$ 
		- for large $n$

## Example Case $c=0$
