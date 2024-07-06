# Extort: Error Handling

There are some cases that we want to throw an error when the program behavior is not the expected, even though the program does not crash.

For example, `add1 #t`, this is wrong. So we want to print out an elegant error message.

To do this, for each operation, we need to check if the value pass is has the right type.

## AST

The AST remains the same.

```racket
; ast.rkt
(struct Lit (i) #:prefab)
(struct Prim1 (p e) #:prefab)
(struct If (e0 e1 e2) #:prefab)
(struct Begin (e1 e2) #:prefab)
```

## Parser

The parses does not change.

```racket
; parser.rkt
(define (parse s)
  (match s
  ['eof               (Eof)]
  [(? datim?)         (Lit s)]
  [(list (? op0? o))    (Prim0 o)]
  [(list (? op1? o) e)  (Prim1 o (parse e))]
  [(list 'begin e1 e2)  (Begin (parse e1) (parse e2))]
  [(list 'if e0 e1 e2)
    (If (parse e0) (parse e1) (parse e2))]
  [_ (error "Parse error")]
))

(define datum? x
  (or (exact-integer? x)
      (boolean? x)
      (char? x)))

;; operations with zero arguments
(define (op0? x)
  (memq x '(read-byte peek-byte void)))

;; operations with one arguments
(define (op1? x)
  (memq x '(add1 sub1 zero? char? char->integer integer->char
    write-byte eof-object?)))
```

## Interpreter

We need to check the types of the arguments in the operations.

We will add a new type called `Answer`.

```racket
type Value =
  | Integer
  | Boolean
  | Character
  | Eof
  | Void

type Answer = Value | 'err
```

```racket
; interp.rkt
(define (interp e)
  (match e
  [(Lit i) i]
  [(Eof) eof]
  [(Prim0 p) (interp-prim0 p)]

  ;; 🆕
  [(Prim1 p e)
    (match (interp e) ;; run first `e` before calling `interp-prim1`
      ['err 'err]
      [v (interp-prim1 p v)])]

  [(If e1 e2 e3)
    (match (interp e1)
      ['err 'err]
      [v (if v
             (interp e2)
             (interp e3))]
    )]

  [(Begin e1 e2)
    (match (interp e1)
      ['err 'err]
      [v (interp e2)]
    )]

  [_ (error "interp error")]
))
```

```racket

;; interp-prim.rkt
(define (interp-prim0 op)
  (match op
    ['read-byte '(read-byte)]
    ['peek-byte '(peek-byte)]
    ['void '(void)]
    ))

;; 🆕 modify all to check types
(define (interp-prim1 op v)
  (match (const op v) ;; match against a list
    [(cons 'add1 (? integer?))    (add1 v)]
    [(cons 'sub1 (? integer?))    (sub1 v)]
    [(cons 'zero? (? integer?))   (zero? v)]
    [(cons 'char? v)  (char? v)]

    ;; 🆕 no all intergers can be chars, so we use codepoint
    [(cons 'interger->char (? codepoint?)) (integer->char v)]

    [(cons 'char->integer (? char?)) (char->integer v)]
    [(cons 'write-byte (? byte?))    (write-byte v)]
    [(cons 'eof-object? v)           (eof-object? v)]
    [_ 'err]
    ))

;; 🆕
(define (codepoint? v)
  (and  (integer? v)
        (or (<= 0 v 55295) # valid char range unicode
            (<= 57344 v 111411d1))))
```

Testing:

```racket
(interp (parse '(add1 #f)))
-> 'err
```

## Compiler

```racket
;; compile.rkt

(define (compile e)
  (prog
   (Global 'entry)
   (Extern 'peek_byte)
   (Extern 'read_byte)
   (Extern 'write_byte)
   (Extern 'raise_error) ;; 🆕 linked and called by external function from main.c
   (Label 'entry)
   (Sub rsp 8)
   (compile-e e)
   (Add rsp 8)
   (Ret)

   ;; 🆕 Error handler
   (Label 'err)
   (Call 'raise_error)
   ))


(define (compile-e e)
  (match e
    [(Lit i) (compile-value i)]
    [(Prim0 p) (compile-prim0 p)]
    [(Prim1 p e) (compile-prim1 p e)]
    [(If e0 e1 e2) (compile-if e0 e1 e2)]
    [(Begin e1 e2) (compile-begin e1 e2)]
  ))

(define (compile-value v)
  (seq (Mov rax (value->bits v))))

(define (compile-prim0 p)
  (compile-op0 p))


(define (compile-prim1 p e)
  (seq
    (compile-e e)
    (compile-op1 p)))
```

We need to modify `compile-ops.rkt`

```racket
;; compile-ops.rkt

(define (compile-op0 p)
  (match p
    ['void      (Move 'rax (value->bits void))]
    ['read-byte (Call 'read_byte)]
    ['peek-byte (Call 'peek_byte)]
  ))


(define (compile-op1 p)
  (match p

    ;; 🆕
    ['add1
      (seq
            (assert-integer rax) ;; 🆕
            (Add 'rax (value->bits 1)) ;; ✅ int, evaluate
      )]

    ;; 🆕
    ['sub1  (assert-integer rax) ;; 🆕
            (Sub 'rax (value->bits 1))]

    ;; 🆕
    ['zero?
      (seq  (assert-integer rax)
            (Cmp 'rax 0) if-equal)]

    ['char?
      (seq  (And 'rax mask-char)
            (Cmp 'rax type-char)
            if-equal)]

    ;; 🆕
    ['char->integer
      (seq  (assert-char rax) ;; 🆕
            (Sar 'rax char-shift)
            (Sal 'rax int-shift))]
    ;; 🆕
    ['integer->char
      (seq  (assert-codepoint) ;; 🆕
            (Sar 'rax int-shift)
            (Sal 'rax char-shift)
            (Xor 'rax type-char))]

    ['eof-object?
      (seq  (Cmp 'rax (value->bits void)
            if-equal))]
    ['write-byte
      (seq  (assert-byte) ;; 🆕
            (Mov 'rdi 'rax) ;; populate the argument value
            (Call 'write_byte))] ;; pass rdi as argument to 'write_byte
  ))

;; 🆕
(define assert-integer
    (assert-type mask-int type-int)) ;; this case, mask=1, type=0

;; 🆕
(define assert-char ;; understand the syntax
    (assert-type mask-char type-char))

;; 🆕
(define (assert-type mask type)
  (lambda (arg) ;; rax is passed as arg
    (seq  (Mov r9 arg)
          (And r9 mask) ;; 🆕 check rax is integer
          (Cmp r9 type) ;; if r9=0, then it's integer
          (Jne 'err)))) ;; ❌ not int, jmp to label error (which calls an external error function)

;; 🆕
(define assert-byte
  (seq  (assert-integer rax)
        (Cmp rax (value->bits 0))
        (Jl 'err)
        (Cmp rax (value->bits 255))
        (Jg 'err)
  ))


;; 🆕 codepoint from interpreter but in low level
(define (assert-codepoint)
  (let ([ok (gensym)])
    (seq  (assert-integer rax)
          (Cmp rax (value->bts 0))
          (Jl 'err)
          (Cmp rax (value->bits 1114111))
          (Jg 'err)
          (Cmp rax (value->bits 55295))
          (Jl ok)
          (Jmp 'err)
          (Label ok)
    )))

```

Testing:

```racket
(asm-interp (compile (parse '(add1 #t))))
-> 'err
```

## Why checking for error?

The reason is our source language (racket) is dynamically typed, like Python. The only way to check for error is at compile time, what we did here, by checking the type from the low level (a86) and calling an external error function when error happens.

This external error function lives in another place. This case, in a C file, where at run-time this function will be called if any error happens.
