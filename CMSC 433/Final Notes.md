# Untitled

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-12-10

---

# Propositional Calculus: Tautologies and Proof

- Deals with statements that can be either true or false
- Establish truth of a given statement
- Fundamental tools for expressing and evaluating logical arguments and deductions
- Two approaches: SAT soving, proof

Tautology: when all are True
Falsiable: when all are False
Satisfiable: when contains at least a True
Unsatisfiable: when is empty


# Sequent and Predicate Calculus

![](20231219051703.png)

![](20231219053347.png)

# Hoare Triples

- wp (weakest prediction). represents minimal condition that ensures the postcondition hodls after executing the givens statement
- sp (strongest postcondition): represents the strongest condition under which the postcondition is guaranteed after executing the statement

![](20231219053853.png)

![](20231219054031.png)
![](20231219055042.png)
# Liquid Haskell

- The Liquid Haskell measure feature enables (certain) functions defined in  
Haskell to be “lifted” into refinement types

To be a valid measure function, a Haskell function must satisfy:  
- One argument, then body  
- Type of argument must be “algebraic”: List , Data type  
- Each constructor in data type must have a single defining equation in  
the function  
- Body of equation can only mention “primitive measures” (i.e. basic  
arithmetic)  
# SAT / SMT Solver

- SMT (Satisfaction Modulo Theories)
- SMT solvers rely on “SAT solvers”
- SAT solvers determine if propositional formulas are satisfiable

- If ¬𝜑 is satisfiable, then 𝜑 is not a tautology: This is because the negation of 𝜑 (¬𝜑) being satisfiable implies that there exists an assignment of truth values to the variables in 𝜑 that makes ¬𝜑 true. If ¬𝜑 is true under some assignment, then 𝜑 is not universally true (tautology) because there is at least one case where ¬𝜑 holds.
- If ¬𝜑 is unsatisfiable, then 𝜑 is a tautology: If ¬𝜑 is unsatisfiable, it means that there is no assignment of truth values to the variables in 𝜑 that makes ¬𝜑 true. In other words, ¬𝜑 is always false. If ¬𝜑 is always false, then 𝜑 must always be true, making 𝜑 a tautology.


- How SMT work? SMT solvers convert decision procedures for sets of atomic predicates in 𝒟 into  decision procedures for quantifier-free formulas.

Basic approach uses SAT solving:
- View quantifier-free formula as formula in propositional calculus, with atomic predicates  treated as propositional variables  
- Use SAT solver on propositional formula to compute satisfying instance; if there is none, quantifier-free formula is unsatisfiable  
- If there is one, compute set of atomic predicates based on truth assignment to give to decision procedure for sets of atomic formulas  
- If the decision procedure returns a state, the quantifier-free formula is satisfiable!  
- If the decision procedure returns UNSAT:  
	- Negation of conjunction of set of atomic formulas must be a tautology!  
	- Conjoin this negation with original quantifier-free formula and repeat
# Conjunctive Normal Form (CNF)


# Z3

Z3 is an SMT solver that accepts statements in some logic and tells you whether or not they can be satisfied, and can find you a model for them if they can be. It's really efficient apparently which is cool because the problems it solves are really asymptotically hard.