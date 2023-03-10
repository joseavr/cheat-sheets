# OCAML NFA
Class: [[OCAML]]
Subject: #
Date: 2023-03-09
Topics: #, #, # 

---

# Intro to Non-Deterministic Finite Automata

Theoretical concept in computer science that defines a mathematical model for recognizing regular languages.

NFA is a finite automaton where for some cases when a single input is given to a single state, the machine goes to more than 1 states, i.e. some of the moves cannot be uniquely determined by the present state and the present input symbol.

NFA = { Q, ∑, ∂, q0, F}

Q → Finite non-empty set of states. 
∑ → Finite non-empty set of input symbols. 
∂ → Transitional Function. 
$q_{0}$ → Beginning state. 
F → Final State

# NFA Example
Let a non-deterministic finite automaton be →

-   Q = {a, b, c}
-   ∑ = {0, 1}
-   q0 = {a}
-   F = {c}

The transition function δ as shown below →
![](../Assets/20230309125709.png)
![[20230309125758.png]]
# NFA with (null) or ∈ move
If any finite automata contains ε (null) move or transaction, then that finite automata is called NFA with ∈ moves.

Consider the following figure of NFA with ∈ move

![](../Assets/20230309124357.png)
![](../Assets/20230309124441.png)

