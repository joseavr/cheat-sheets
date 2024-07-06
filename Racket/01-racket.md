# Untitled

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2024-05-30

---

# Conditionals

```racket
(if (condition) expression1 expression2)
```

# Conditional Matching


# Functions

```racket
(define (filter5 p l))
```


# Lists


## `cdr` (cudder)

Takes the tail of a list

```racket

```

## `car`

Takes the head of a list

```racket

```


# High Order Functions

## `map`

## `foldl`

The foldl in racket

```rkt
(foldl (lambda (x acc) (+ x acc)) 0 l)
```

*Example:*

```racket
(filter5 (lambda (x) (> x 0)) '(10 -4 0 2 -5))
```

Example:

```rkt
(define (filter5 p l)  
 (fold l (lambda (x acc) (if (p x)  (cons x acc) acc)) 
'() l))
```

