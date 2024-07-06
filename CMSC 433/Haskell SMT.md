# SMT

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-11-16

---

# Intro 

- SMT solvers rely on "SAT solvers"
- SAT solvers determine if porpositional formulas are satisfiable (true table)

The SAT problem
- Given: propositional formula p
- Determine: is p satisfiable
	- is there `state` such that `state`|=`formula`
	- SAT solvers returns it

SAT was the first NP-complete problem


# Conjunctive Normal Form (CNF)

- `OR` inside and `AND` outside does not violate the CNF

(p v q) ^ (~q) is in CNF
(p ^ q) v (~p) is not in CNF

**State:** 
- variables, boolean, values

**Literal:**
- It is a formula of form either p or ~p, where p is a variable

**Clause:**
- It is a disjunction of a finite number of literals
- e.g. p v ~q v r
- e.g. { {p,q}, {~q}} = {p,q} ^ {~q}
- = (p v q) ^ (~q)

Given: (p v ~q) ^  v ^ (r v ~p)
clause = {{p,~q}, {r}, {r,~p}}

Note: 
- Clause of {} = false
- Formula of {} = true


# How to Transform Formula Into CNF

1. Drive negations inside using DeMorgan
	- ~(pvq) = (~p) v (~q)
2. More `^` outside of `v` using distribution
	- p v (q ^ r) = (p v q) ^ (p v r)
	- if p is true then whole is True because `or`
3. Apply distribution exhaustively until no `^` inside `v`


**When does a state make S={$C_{1}$, ... , Cn} trie?**:
- State must make each Cn true
- State makes Ci = { $l_{i}$ ... $l_{j}$}
	- iff it makes at least 1 of the $\ln_{ij}$ true


#### Example
Suppose S = { {p, ~q, r}, {~q, ~r}, {~p,q}}
=> (p or ~q or r) AND (~q or ~r) AND (~p or q)

Does $state_{1}$ where $state(p)=1$, $state(q)=1$ , $state(r)=0$ satisfies S?
- $state_{1}$ |= {p,~q,r} ? Yes
- $state_{1}$ |= {~q, ~r} ? Yes
- $state_{1}$ |= {~p,q}? Yes
- So answers is yes!

Does $state_{2}$ where $state_{2}(p)=1$, $state_{2}(q)=0$, $state_{2}(r)=0$ satisfies S?
- $state_{2}$ |= {p,~q,r}? Yes
- $state_{2}$ |= {~q, ~r}? Yes
- $state_{3}$ |= {~p,q}? No
- So answer is No!