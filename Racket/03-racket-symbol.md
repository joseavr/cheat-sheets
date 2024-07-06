📚Class:

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section:

🗓️Date: 2024-05-30

---

# Symbols

They are like strings or **Literals**

```rkt
'aa
-> 'aa

'+
-> '+

'"hello"
-> "hello"
```

Since `()` in racket evaluates, using `'()` prevents evaluation.

```rkt
'(1 2 3)  is the same as (list 1 2 3)
```

Function that takes two arguments and sum:

```rkt
(+ 1 2)
-> 3
```

```rkt
'(+ 1 2)
-> '(+ 1 2)


'(x y z)
-> (list 'x 'y 'z)
```

```rkt
'()
'((1)) ; this is (list '(1)); (list (list 1))


(list (+ 1 2))
-> 3

'((+ 1 2)) ; this is (list '(+ 1 2))
-> '((+ 1 2))

(quote +)
-> '+

```

For next: we can parse this

```rkt
'(define (add m n)  (+ n m))
```
