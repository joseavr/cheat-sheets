# M2 Cheat Sheets

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-04-19

---
# Lemmas

## Lemma 1
if $a\mid c$ and $b\mid c$ and gcd(a,b)=1
- then $ab\mid c$

## Lemma 2
Let a,c,k ints
- (a,c) = (a + ck, c)


# Inverse of a module m

# Chapter 5: Applications of Congruences

## Dibisiblity by 7


## Divisiblity by 11
A number $abcdf$ with an alternative sum $a-b+c-d+f = x$ 
- if $11 \mid x$, then divisible by 11


## Divisibility by 13



# Chapter 6: Special Congruences

## Theorem 6.1: Wilson's Theorem. 
If $p$ is prime, then $(p - 1)! \equiv -1(mod\>p)$.

## Theorem 6.3: Fermat's Little Theorem
If $p$ is prime and a is an integer with $p \nmid a$, 
- then $a^{P-1} = 1 (mod\>p)$

## Theorem 6.4
If p is prime and a is a positive integer, 
- then $a^{P} \equiv a (mod\>p)$

Example:
- By Fermat, we know that $3^{11-1} = 3^{10}= 1 (mod\>11)$ 
- Hence, $3^{201} =( 3^{10} )^{20} \cdot 3 \equiv 3 (mod\>11)$

## Theorem 6.5
If p is prime and a is an integer such that $p \nmid a$, 
- then $a^{P-2}$ is an inverse of a modulo p.

Example:
By Theorem 6.5, we know that $2^{11-2} = 2^{9} = 512 = 6 (mod\>11)$ is an inverse of 2 modulo 11.

# Chapter 6.2 Pseudoprimes
If $n$ is a composite positive integer and $b^{n} = b\>(mod\>n)$, 
- then $n$ is called a pseudoprime to the base $b$.


# Chapter 6.3: Euler Phi Function

If p is a prime
- $\phi(p) = p-1$

Primes

| $n$         | 1   | 2   | 3   | 5   | 7   | 11  | 13  |
| --------- | --- | --- | --- | --- | --- | --- | --- |
| $\phi(p)$       | 1   | 1   | 2   | 4   | 6   | 10  | 12  |

Composites

| $n$       | 4   | 6   | 8   | 9   | 10  | 12  |
| --------- | --- | --- | --- | --- | --- | --- |
| $\phi(p)$ | 2   | 2   | 4   | 4   | 4   | 4   |

## Euler Theorem
If $m \geq 0$ and $a$ is an integer with $(a, m) = 1$
- then $a^{\phi(m)} \equiv 1\>(mod\>m)$
