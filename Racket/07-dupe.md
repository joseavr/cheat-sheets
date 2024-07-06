# Dupe: Integers and Booleans

Adding boolean types to our compiler

How can we assume types? In Dupe, we must follow these rules

```racket
[..., 0] ; if the most significant right value is 0, then treat this as Int

[..., 1] ; if M.S.R is 1, then treat this as Bool
[..., 0, 1] ; if two last are 01, then #t
[..., 1, 1] ; if two last are 11, then #f
```

## Values vs Bit Representation

```racket
(define (bits->value b)
  (cond
    [(= b (value->bits #t)) #t]
    [(= b (value->bits #f)) #f]
    [(int-bits? b) (arithmetic-shift b -1) ]
    [else (error "invalid bits")]
    ))

(define (value->bits v)
  (cond
    [(eq? v #t) #b01]
    [(eq? v #f) #b11]
    [(integer? v) (arithmetic-shift v 1)]
  ))
```

**Note:** To understand this, in order to add types, we will add a tag at the end of the value of a register.

For example: let number 5, which is 0101. How do we know this is a number? Well, add a tag 0 (or shift left)

Given value 5 -> 0101 -> add tag -> 0101[0]. This in bits 01010 is 10.

In same opposite way, given bits 01010 -> right shift -> 0101 -> 5

So 5 -> value->bits -> 10
And 10 -> bits->value -> 5

## AST

```racket
; ast.rkt

#lang racket
(provide Lit Prim1 IfZero) ;; make this module visibile

(struct Lit (i) #:prefab)
(struct Prim1 (p e) #:prefab)
(struct If (e0 e1 e2) #:prefab) ; 🆕
```

## Parser

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
  [(list 'if e0 e1 e2)
    (If (parse e0) (parse e1) (parse e2))]

  [_ (error "Parse error")]
))
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
  [(If e1 e2 e3)
    (if (interp e1) (interp e2) (interp e3))]


  [_ (error "interp error")]
))
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


(define (compile-e e)
  (match e
    [(Lit i) (compile-value i)]
    [(Prim1 op e) (compile-prim p e)]

    ; 🆕
    [(If e0 e1 e2) (compile-if e0 e1 e2)]
  ))

; 🆕
(define (compile-value v)
  (seq (Mov rax (value->bits v))))
 

(define (compile-prim1 p e)
  (seq
    (compile-e e)     ;; needed for recursive call
    (compile-op1 p)))

(define (compile-op1 p)
  (match p
    ['add1 (Add 'rax 1)]
  ))

; 🆕
(define (compile-if e0 e1 e2) (
  (let (
    (l1 (gensym 'if))  
    (l2 (gensym 'end))
    )
    (seq 
      (compile-e e0)
      (Cmp rax (value->bits #f)) ; if rax = false
      (Je l1)
      (compile-e e1)
      (Jmp l2)
      (Label l1)
      (compile-e e2)
      (Label l2)
    ))
))
```

Now we can test this:
```racket
;; compile-time: output of encoded program
(asm-interp (compile (parse '(if #f 10 20))))
-> 40

;; runtime: expect of decoded program with types
(bits->value (asm-interp (compile (parse '(if #f 10 20)))))
-> 20
```

## Runtime

How does know at runtime the type? At runtime we can check the types:

```C
void print_result(val_t x)
{
  // check the type at runtime
  switch (val_typeof(x)) {
  case T_INT:
    // underhood eliminates the type bit and extracts the number
    printf("%" PRId64, val_unwrap_int(x));
    break;
  case T_BOOL:    
    printf(val_unwrap_bool(x) ? "#t" : "#f");
    break;
  case T_INVALID:
    printf("internal error");
  }
}
```

Implementation of the type checking:

```C
int64_t val_unwrap_int(val_t x)
{
  return x >> int_shift;
}
val_t val_wrap_int(int64_t i)
{
  return (i << int_shift) | int_type_tag;
}
int val_unwrap_bool(val_t x)
{
  return x == val_true;
}
val_t val_wrap_bool(int b)
{
  return b ? val_true : val_false;
}
```
