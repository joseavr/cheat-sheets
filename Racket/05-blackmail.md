# Blackmail

Blackmail is the continuation of abscond but added summation functionalities

## AST

```racket
; ast.rkt

#lang racket
(provide Lit Prim1) ;; make this module visibile

(struct Lit (i) #:prefab)
(struct Prim1 (p e) #:prefab)
```

We can run the following:

```racket
(Prim1 'sub1 10)
-> #s(Prim1 sub1 10) ;; parser ✅

(Prim1 'add1 10)
-> #s(Prim1 add1 10) ;; parser ✅

(Prim1 2 10)
-> #s(Prim1 2 10)  ;; however our parser will reject this ❌
```

## Parser

Now it can parse summation functions.

```racket
; parser.rkt

#lang racket
(provide parse)
(require "ast.rkt")

(define (parse s)
  (match s
  [(? exact-integer?) (Lit s)]

  ;; 🆕
  [(list (? op1? o) e) (Prim1 o (parse e))]
  ;; (? op1? o) means that must be a valid argument operator: `add1`
  ;; e is the number passed to `add1`: `add1 10`

  [_ (error "Parse error")]
))

(define (op1? x)
  (memq x '(add1 sub1))
  ; is x a member either `add1` or `sub1`
  ; if yes, then return the operator matched
  )
```

If we run this:

```racket
(parse '(sub1 42))
-> '#s(Prim1 sub1 #s(Lit 42))


(parse '(add1 sub1))
-> Parse error

(parse '(add1 (sub1 42)))
-> '#s(Prim1 add1 #s(Prim1 sub1 #s(Lit 42)))
```

## Interpreter

```racket
; interp.rkt

#lang racket
(provide interp)
(require "ast.rkt")
(require "interp-prim1")

;; Expr -> Integer
(define (interp e)
  (match e
  [(Lit i) i]

  ;; 🆕
  [(Prim1 p e) (interp-prim1 p (interp p e))]

  [_ (error "interp error")]
))
```

We also need the inter-prim1.rkt for the interpreter

```racket
; interp-prim1.rkt

#lang racket
(provide interp-prim1)

(define (interp-prim1 op i)
  (match op
  ['add1 (add1 i)]
  ))
```

If we run the this:

```racket
;; tracking the code
(interp (parse '(add1 42)))
-> (interp '#s(Prim1 add1 #s(Lit 42)))
-> (interp-prim1 'add1 42)
-> (add1 42)
-> 43

;; Could also do, skipping the parse
(interp (Prim1 'add1 (Lit 42)))
-> 43
```

## Compiler

```racket
#lang racket
(provide (all-defined-out))
(require "ast.rkt")
(require a86/ast)

;; boilerplate
(define (compile e)
  (prog
   (Global 'entry)
   (Label 'entry)
   (compile-e e)
   (Ret)
   ))

;; code here
(define (compile-e e)
  (match e
    [(Lit i) (Mov 'rax i)]

    ;; 🆕
    [(Prim1 op e) (compile-prim p e)]
  ))

;; 🆕
(define (compile-prim p e)
  (seq
    (compile-e e)     ;; needed for recursive call
    (compile-op1 p)))

(define (compile-op1 p)
  (match p
    ['add1 (Add 'rax 1)]
  ))

```

Now running this:

```racket
(asm-interp (compile (parse '(add1 10))))
-> 11


(asm-interp (compile (parse '(add1 (add1 41)))))
-> 43
```
