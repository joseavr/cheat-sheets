# 🔰 Algorithms Dijkstra

📚Class: CMSC 351 Algorithms

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/CMSC%20351%20Algorithms/Algorithms.md">Algorithms</a>

✏️Section: 0301

🗓️Date: 2023-04-16

---
# 🎬 Intro to Dijkstra
- Dijkstra applies to **weighted** and **directed/undirected** graphs
- Dijkstra applies to **unweighted** and **directed/undirected** graphs
	- Set all the weights to 1
- Dijsktra is optimal (all distances returned are minimal)



# ⏳ Running Time
- `Fib Heap`
	- $Θ\left( E + V \log V  \right)$
- `Min Heap`
	- $Θ\left( (E + V) \log V  \right)$
	- $Θ\left( E  \log V  \right)$
- `Without Heap`
	- $Θ\left( V^{2}  \right)$

**Note**:
V = number of vertices in the graph  
E = number of edges in the graph

# ⌛️ Space Time
- $Θ \left( V + E  \right)$


# 🤷🏻‍♂️ What is Dijkstra
Dijkstra’s Algorithm is essentially an extension of the shortest path algorithm in which the graph is weighted. In this case instead of looking for a shortest path we are looking for a path of minimal weight.

What we’ll actually do is better, we’ll find a shortest weight tree which is a tree that is a subgraph of the graph such that, treating the starting vertex as the root, explicitly shows us how to get to every other vertex with minimal weight.

TODO

# Pseudocode
```python

```

```python

```

