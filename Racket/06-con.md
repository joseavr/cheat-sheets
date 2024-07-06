# Con (Conditional Execution)

`Con` adds conditional to our target language.

The syntax: `(if (zero? e0) e1 e2)`

Parsed in AST as `(IfZero e0 e1 e2)`

For example:

```racket
(if (zero? 0) (add1 2) 4)

;; parsed in AST
-> (IfZero 0 (add1 2) 4)
```

## AST

```racket
; ast.rkt

#lang racket
(provide Lit Prim1 IfZero) ;; make this module visibile

(struct Lit (i) #:prefab)
(struct Prim1 (p e) #:prefab)
(struct IfZero (e0 e1 e2) #:prefab) ; 🆕
```

We can run the following and get the following AST:

```racket
(IfZero '(zero? 0) 1 2)
-> #s(IfZero (zer0? 0) 1 2)
```

## Parser

Now it can parse conditionals.

We can run this to parse to an AST

```racket
; parser.rkt

#lang racket
(provide parse)
(require "ast.rkt")

(define (parse s)
  (match s
  [(? exact-integer?) (Lit s)]
  [(list (? op1? o) e) (Prim1 o (parse e))]

  ;; 🆕
  [(list 'if (list 'zero? e0) e1 e2)
    (IfZero (parse e0) (parse e1) (parse e2))]

  [_ (error "Parse error")]
))
```

If we run this:

```racket
(parse '(if (zero? 0) 1 2))
-> #s(IfZero #s(Lit 0) #s(Lit 1) #s(Lit 2))
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
  [(Prim1 p e) (interp-prim1 p (interp p e))]

  ;; 🆕
  [(ifZero e0 e1 e2)
    (if (zero? (interp e0)) (interp e1) (interp e2))]

  [_ (error "interp error")]
))
```

If we run the this:

```racket
(interp (parse '(if (zero? 0) 1 2)))
-> 1
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
    [(Prim1 op e) (compile-prim p e)]

    ;; 🆕
    [(IfZero e0 e1 e2) (compile-ifzero e0 e1 e2)]
  ))

;; 🆕
(define (compile-prim1 p e)
  (seq
    (compile-e e)     ;; needed for recursive call
    (compile-op1 p)))

(define (compile-op1 p)
  (match p
    ['add1 (Add 'rax 1)]
  ))

;; 🆕
(define (compile-ifzero e0 e1 e2)
  (seq
    (compile-e e0) ;; rax <- result
    (Cmp rax 0)
    (Jne 'else) ;; rax != 0, jmp to 'else' branch

    ;; `then` branch
    (compile-e e1)
    (Jmp 'end)

    ;; `else` branch
    (Label 'else)
    (compile-e e2)

    ;; 'end' branch
    (Label 'end)
    ))
```

However, here we have an issue when having nested if statements, so the program, at the runtime, throws the error: `duplicate label declaration found: 'else`

To fix thi, we must use gensym, to create unique symbol for the label:

```racket
(define (compile-ifzero e0 e1 e2)

  (let (
    (l1 (gensym 'else))
    (l2 (gensym 'end))
    )

    (seq
      (compile-e e0) ;; rax <- result
      (Cmp rax 0)
      (Jne l1) ;; rax != 0, jmp to 'else' branch

      ;; `then` branch
      (compile-e e1)
      (Jmp l2) ; jmp to 'end'

      ;; `else` branch
      (Label l1)
      (compile-e e2)

      ;; 'end' branch
      (Label l2))
  ))
```

Now running this:

```racket
(asm-interp (compile (parse '(if (zero? (if (zero? 0) 1 2)) 1 2))))
-> 2
```
