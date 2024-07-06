# Untitled

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2024-05-30

---

# Struct

```rkt
(struct Nil ())
(struct Node (i rest))

(Nil)
(Node 10 NIl)
(node 10 (Node 20 (Nil)))

(Node-i (Node 10 (Nil)))
(Node-rest (Node 10 (Node 20 Nil)))

(define (sum l)
  (math l
    [(Nil) 0]
    [(Node i r) (+ i (sum r))]
  )

)

```