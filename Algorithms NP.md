# Algorithms Non Deterministic Polynomial

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-05-04

---
# 🎬 Intro to NP


# Traveling Salesman Problem
- Also known as TSP
- We have number of ciities
- Traveling salesman starts at city 1 and goes thru every city exactoy once before returning to city 1. (Hamiltonian )
- Cities are vertices

![[Pasted image 20230504111100.png]]


Optimal Tour
![[Pasted image 20230504111111.png]]

## Decision Problem
- What is the optimal (minimum total distance) TSP tour?
	- In other words, is there a tour whose total distance is <= k

## Proof/Witness/Certificate
- Given a decision problem and an instance of that problem, can we find a proof (or witness, or certificate) showing that the decision is YES?

- I (instance) = {-1,4,17,-3,10}  
- The subset {-1,4,-3}is a witness (also called a certificate, or proof)  
- {17,-3} is NOT a witness/certificate

Decision problem  
- If we have a (valid) witness/certificate answer is YES  
- If we do not have a (valid) witness/certificate, we cannot decide that the answer is NO (it may be NO, it may be  
YES)

# P
- Example: Given a list L, is it sorted?
- If we run buble sort, and we found no sorted, then asnwer is NO

## Subset
- The other is the question {is there a subset where sum is 0}
- Certificate means the potential solution that answer YES or NO
- {-1+4-3 = 0} is a ceritificate


## Hamiltonian Cycle
- 

## Clique
- k-clique, a subgraph that has k vertices connected
- A graph with Clique of size 3

![[Pasted image 20230504112107.png]]

- A graph with Clique of size 4
![[Pasted image 20230504112208.png]]

# NP
- Non Deterministic Polynomial
- NP = { Q is a deciosion problem, there is a NP algo that outputs YES or NO for given instnace of the problem and potential witness/certificate for that instance}
- Have the right to guess the solution
- There is a polynomial algo. tha twill check if your guess is correct or not
- Is it easier than no  having a guess? Yes, NP

## Subset Problem
- asda
- Verifier algorithm: loop all elements and sum, check if its 0, then output YES or NO (O(n))

## Clique
- Is in NP
- Verifier algorithm: check they are all connected, runs O(n^2) worst case

# P vs NP
- P is included in NP
- Uknown if P = NP or P != NP
- Most people believe P != NP

## Proof
- TODO


# Reduction
- Reductions tries to converts a function to another fucntion that gives the same solutionq
