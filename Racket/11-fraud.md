# Fraud

Adds local binding and ability to use binary operations to our target language.

Some examples:

```racket
(let ((x e1)) x) ;; evaluates to e1
;; let x = e1 in x (ocaml)

(let ((x 7)) (let ((y 2)) x))
-> 7

(let ((x 7)) (let ((x 2)) x)) ;; inner 'x' has more precedence -> shadowing
(let ((x 7)) 2)
-> 2
```

## AST

```racket

; ast.rkt
(struct Eof () #:prefab)
(struct Lit (i) #:prefab)
(struct Prim0 (p e) #;prefab)
(struct Prim1 (p e) #:prefab)
(struct If (e0 e1 e2) #:prefab)
(struct Begin (e1 e2) #:prefab)

;; 🆕
(struct Let (x e1 e2) #:prefab)
(struct Var (x) #:prefab)
```

## Parser

```racket
; parser.rkt
(define (parse s)
  (match s
  ['eof                     (Eof)]
  [(? datum?)               (Lit s)]
  [(? symbol?)              (Var s)] ;; 🆕
  [(list (? op0? o))        (Prim0 o)]
  [(list (? op1? o) e)      (Prim1 o (parse e))]

  ;; 🆕
  [(list (? op2? o) e1 e2)  (Prim2 o (parse e1) (parse e2))]

  [(list 'begin e1 e2)      (Begin (parse e1) (parse e2))]
  [(list 'if e0 e1 e2)
    (If (parse e0) (parse e1) (parse e2))]

  ;; 🆕
  [(list 'let x (list (list (? symbol? x) e1)) e2)
    (Let x (parse e1) (parse 2))]

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

;; 🆕
(define (op2? x)
  (memq x '(+ - < =)))
```

Testing:

```racket
(parse '(+ 10 20))
-> '#s(Prim2 + #s(Lit 10) #s(Lit 20))

(parse '(let ((x 10)) x))
-> '#s(Let x #s(Lit 10) #s(Var x))
```

## Interpreter

```racket
; interp.rkt

;; 🆕 now use new interp-env
(define (interp e)
  (interp-env e '() ))

;; 🆕
(define (interp-env e r)
  (match e
  [(Lit i) i]
  [(Eof) eof]

  ;; 🆕
  [(Var x) (lookup r x)]

  [(Prim0 p) (interp-prim0 p)]
  [(Prim1 p e)
    (match (interp-env e r) ;; 🆕 added interp-env
      ['err 'err]
      [v (interp-prim1 p v)])]

  ;; 🆕
  [(Prim2 p e)
    (match (interp-env e1 r)
      ['err 'err]
      [v1
        (match (interp-env e2 r))
          ['err 'err]
          [v2 (interp-prim2 p v1 v2)]
      ])
  ]

  [(If e1 e2 e3)
    (match (interp-env e1 r) ;; 🆕 interp-env
      ['err 'err]
      [v (if v
             (interp-env e2 r) ;; 🆕 interp-env
             (interp-env e3 r))] ;; 🆕 interp-env
    )]

  [(Begin e1 e2)
    (match (interp-env e1 r) ;; 🆕 interp-env
      ['err 'err]
      [v (interp-env e2 r)] ;; 🆕 interp-env
    )]

  ;; 🆕
  [(Let x e1 e2)
    (match (interp-env e1 r)
      ['err 'err]
      [v (interp-env e2 (ext r x v))]
    )]

  [_ (error "interp error")]
))


;; 🆕
(define (lookup r x)
  (match r
    ['() 'err]
    [(cons (list y val) r)
        (if (symbol=? x y)
            val
            (lookup r x))]
  ))

;; 🆕
(define (ext r x v)
  (cons (list x v) r))
```

What does lookup and ext? Here some examples

```racket
;; 1.
(ext (ext '() 'x 10) 'y 20)
-> ((y 20) (x 10)) ;; adds 20 to the beg of the list

(lookup
  (exet (ext '() 'x 10) 'y 20)
  'x) ;; find the first in the list
-> 10

;; 2,
(ext (ext (ext '() 'x 10) 'y  20) 'x 30)
-> ((x 30) (y 20) (x 10))

(lookup
  (ext (ext (ext '() 'x 10) 'y  20) 'x 30)
  'x)
-> 30
```

We need to add `interp-prim2` in `interp-prim.rkt`:

```racket
;; interp-prim.rkt

(define (interp-prim0 op)
  (match op
    ['read-byte '(read-byte)]
    ['peek-byte '(peek-byte)]
    ['void '(void)]
    ))

(define (interp-prim1 op v)
  (match (list op v) ;; match against a list
    [(list 'add1 (? integer?))    (add1 v)]
    [(list 'sub1 (? integer?))    (sub1 v)]
    [(list 'zero? (? integer?))   (zero? v)]
    [(list 'char? v)  (char? v)]
    [(list 'interger->char (? codepoint?))    (integer->char v)]
    [(list 'char->integer (? char?))          (char->integer v)]
    [(list 'write-byte (? byte?))             (write-byte v)]
    [(list 'eof-object? v)                    (eof-object? v)]
    [_ 'err]
    ))

;; 🆕
(define (interp-prim2 p v1 v2)
  (match (list op v1 v2)
    [(list '+ (? interger?) (?integer?))    (+ v1 v2)]
    [(list '- (? integer?) (? integer?))    (- v1 v2)]
    [(list '< (? integer?) (? integer?))    (< v1 v2)]
    [(list '= (? integer?) (? integer))     (= v1 v2)]
    [_ 'err]
    ))

(define (codepoint? v)
  (and  (integer? v)
        (or (<= 0 v 55295) # valid char range unicode
            (<= 57344 v 111411d1))))
```

Testing:

```racket
(interp (parse '(- #t 20)))
-> 'err

(interp (parse '(let ((x  10)) x)))
-> 10
```

## The environment issue

In the interpreter, we decided the environment to store a list of list to keep track of the `Let` bindings. 

```racket
((x 10) (y 20) (z 10))
```

However, in compiled binaries, this data structure is hard to implement.

However, we can do better. 

Normally, our let binding is represented like this: 

```racket
(let ((p ...))
  ...
  (let ((x ...))
  ...
    (let ((y ...))
      ... x ...)))
-> ((y ...) (x ...) (p ...)) ;; then search O(n) for x
```

Observing the new way.
```racket
;; better
(let ((_ ...))
  ...
  (let ((_ ...))
  ...
    (let ((_ ...))
      ... (Var 1) ...)))
-> ((_ ...) (_ ...) (_ ...)) ;; search at pos. 1
```

The new way stores the position of variable to be bound, but notice that we no longer store the variable symbol.

This is O(1) lookup.

## Translate

We will add a new file called translate to parse this new environment.

```racket
(define (translate e)
  (translate-e e '()))

(define (translate-e e r)
  (match e
    [(Eof)        e]
    [(Lit d)      e]
    [(Prim0 p)    e]
    [(Prim1 p e0)
        (Prim1 p (translate-e e0 r))]
    [(Prim2 p e0 e1)
        (Prim2 p
                  (translate-e e0 r)
                  (translate-e e1 r))]
    [(If e0 e1 e2)
        (If  (translate-e e0 r)
             (translate-e e1 r)
             (translate-e e2 r))]
    [(Begin e0 e1)
        (Begin  (translate-e e0 r)
                (translate-e e1 r))]
    [(Let x e0 e1)
        (Let '_
                (translate-e e0 r)
                (translate-e e1 (cons x r)))]
    [(Var x)
        (Var (lexical-addres x r))]            
  ))

(define (lexical-address x r)
  (match r
    [(cons y r)     ()]
    [(match (symbol=? x y)
        [#t 0]
        [$f (add1 (lexical-address x r))]
        )]
    ))
```

Some testing:

```racket
(parse '(let ((x 10 )) x))
-> '#s(Let x #s(Lit 10) #s(Var x))

(translate (parse '(let ((x 10 )) x)))
-> '#s(Let _  #s(Lit 10) #s(Var 0))

(translate (parse '(let ((x 10))
                      (let ((y 20))
                        y))))
-> '#s(Let _ #s(Lit 10) #s(Let _ #s(Lit 20) #s(Var 0)))
```

**Note:** The lexical address function is key to assign the index position for the binding.

```racket
(lexical-address 'a '(a b c x))
-> 0

(lexical-address 'x '(a b c x))
-> 3
```

## New Interpreter

Now with this new functionality translate, we need to modify the `interpreter.rkt`

```racket
; interp-lexical.rkt

(define (interp e)
  (interp-env e '() ))

(define (interp-env e r)
  (match e
  [(Lit i) i]
  [(Eof) eof]

  [(Var x) (list-ref r x)] ;; 🆕 list-ref instead of lookup()

  [(Prim0 p) (interp-prim0 p)]
  [(Prim1 p e)
    (match (interp-env e r)
      ['err 'err]
      [v (interp-prim1 p v)])]

  [(Prim2 p e)
    (match (interp-env e1 r)
      ['err 'err]
      [v1
        (match (interp-env e2 r))
          ['err 'err]
          [v2 (interp-prim2 p v1 v2)]
      ])
  ]

  [(If e1 e2 e3)
    (match (interp-env e1 r) 
      ['err 'err]
      [v (if v
             (interp-env e2 r)
             (interp-env e3 r))]
    )]

  [(Begin e1 e2)
    (match (interp-env e1 r) 
      ['err 'err]
      [v (interp-env e2 r)] 
    )]

  [(Let '_ e1 e2)
    (match (interp-env e1 r)
      ['err 'err]
      [v (interp-env e2 (cons v r))] ;; 🆕 replaced ext()
    )]

  [_ (error "interp error")]
))
```

Testing:

```racket
(interp (parse '(let ((x 10))
                       (let ((y 20))
                         (let ((z 30))
                           y)))))
-> 20

(translate (parse '(let ((x 10))
                      (let ((y 20))
                          (let ((z 30))
                            x)))))
-> #s(Let _ #s(Lit 10) #s(Let _ #s(Lit 20) #s(Let _ #s(Lit 30) #s(Var 2))))
;; (30,20,10)
;;  0  1  2
```

## Stack alignment

We know that the stack must be aligned to 16-bytes to call any function.

Thus we will dynamically align it:

```racket
Mov r15 rsp     ;; get the top of the stack
And r15 #b1000  ;; dynamically align
                ;; if r15 = #b1000 -> 8 (divisible by 8)
                ;; otherwise -> 0 (divisible by 16) 
Sub rsp r15     ;; decrement stack by r15 (8 or 0 bytes) -> aligned
Call foo        ;; safely call foo()
Add rsp r15     ;; put pointer back
```

We can break down this code into `pad-stack` and `unpad-stack`

```racket
(define (pad-stack)
    (seq  (mov r14 rsp)
          (And r15 #b1000)
          (Sub rsp r15)))

(define (unpad-stack) 
    (seq Add rsp r15))
```

Here an example how to use them

```racket
(seq  
    assert-byte
    pad-stack     ;; 🆕
    (Mov rdi rax)
    (Call write_byte)
    unpad-stack)  ;; 🆕
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
   (Extern 'raise_error)
   (Label 'entry)

   ;; stack is 8-byte aligned here
   ;; 🆕 save callee-saved register
   (Push r15) ;; stack 16-byte aligned ✅

   (compile-e e '()) ;; 🆕 compile-e with 2 args

   ;; 🆕 restore calle-save register
   (Pop r15)
   (Ret)

   ;; Error handler
   (Label 'err)
   pad-stack  ;; 🆕
   (Call 'raise_error)
   ;; don't have to unpad since it's error, program termines
   ))


(define (compile-e e c) ;; 🆕 compile-2 with 2 args
  (match e
    [(Lit i)       (compile-value i)]
    [(Eof)         (compile-value eof)]
    [(Var x)       (compile-variable x c)] ;; 🆕
    [(Prim0 p)     (compile-prim0 p)]
    [(Prim1 p e)   (compile-prim1 p e c)] ;; 🆕 compile-prim1 3 args
    [(Prim2 p e1 e2) (compile-prim2 p e1 e2 c)] ;; 🆕
    [(If e0 e1 e2) (compile-if e0 e1 e2 c)] ;; 🆕 compile-if 4 args
    [(Begin e1 e2) (compile-begin e1 e2 c)] ;; 🆕 compiile-begin 3 args
    [(Let x e1 e2) (compile-let x e1 e2 c)] ;; 🆕
  ))


(define (compile-value v)
  (seq (Mov rax (value->bits v))))

;; 🆕 lookup the environment and get the index i
;; store in rax the index position i from the stack 
(define (compile-variable x c)
  (let ((i (lookup x c)))   
        (seq (Mov rax (Offset rsp i)))
        ))

(define (compile-prim0 p)
  (compile-op0 p))


(define (compile-prim1 p e c) ;; 🆕 compile-prim1 3 args
  (seq
    (compile-e e c)
    (compile-op1 p)))

;; 🆕
(define (compile-prim2 p e1 e2 c)
  (seq 
    (compile-e e1 c)
    (Push rax) ;; since e1 and e2 evaluated needs rax, we push the first to stack to keep track 
    (compile-e e2 (const (gensym) c)) ;; 🆕 e2 evualted stored in rax
    (compile-op2 p))) ;; call operant, i.e +, takes both args1 (in stack) and arg2 (in rax)


(define (compile-if e1 e2 e3c)
  (let (
          (li (gensym 'if))
          (l2 (gensym 'if))
       )
    ;; in
    (seq  (compile-e e1 c)
          (Cmp rax (value->bits #f))
          (Je l1)
          (compile-e e2 c)
          (Jmp l2)
          (Label l1)
          (compile-e e3 c)
          (Label l2)
    )))

;; 🆕
(define (compile-begin e1 e2 c)
  (seq  (compile-e e1 c)
        (compile-e e2 c)))

;; 🆕
(define (compile-let x e1 e2 c)
  (seq  (compile-e e1 c) ;; let x = 10 + 20
        (Push rax)       ;; push 30 (we need value later)
        (compile-e e2 (cons x c))
        (Add rsp 8) ;; we could (Pop rax) but we dont want to replace rax
  ))

;; 🆕
(define (lookup x cenv)
  (match cenv
    ['() (error "undefined variable:" x)]
    [(cons y rest)
        (match (eq? x y)
          [#t 0]
          [#f (+ 8 (lookup x rest))]
        )]      
  ))
```
 
We need to modify `compile-ops.rkt` as well

```racket
;; compile-ops.rkt

(define (compile-op0 p)
  (match p
    ['void      (seq (Move 'rax (value->bits void)))]

    ;;  🆕 modified read-byte
    ['read-byte 
        (seq  pad-stack
              (Call 'read_byte)
              unpad-stack)]

    ;; 🆕 modified peek-byte          
    ['peek-byte 
        (seq  pad-stack
              (Call 'peek_byte)
              unpad-stack)]
  ))


(define (compile-op1 p)
  (match p
    ['add1
      (seq  (assert-integer rax) 
            (Add 'rax (value->bits 1)) ;; ✅ int, evaluate
      )]

    ['sub1  
      (seq  (assert-integer rax) 
            (Sub 'rax (value->bits 1)))]

    ['zero?
      (seq  (assert-integer rax)
            (Cmp 'rax 0) 
            if-equal)]

    ['char?
      (seq  (And 'rax mask-char)
            (Cmp 'rax type-char)
            if-equal)]

    ['char->integer
      (seq  (assert-char rax) 
            (Sar 'rax char-shift)
            (Sal 'rax int-shift))]

    ['integer->char
      (seq  (assert-codepoint)
            (Sar 'rax int-shift)
            (Sal 'rax char-shift)
            (Xor 'rax type-char))]

    ['eof-object?
      (seq  (Cmp 'rax (value->bits void)
            if-equal))]
    ['write-byte
      (seq  (assert-byte) 
            (Mov 'rdi 'rax) ;; populate the argument value
            (Call 'write_byte))] ;; pass rdi as argument to 'write_byte
  ))

;; 🆕
(define (compile-op2 p)
  (math p
    ['+  
      (seq  (Pop r8)
            (assert-integer r8)
            (assert-integer rax)
            (Add rax r8))]
    ['- 
      (seq  (Pop r8)
            (assert-integer r8)
            (assert-integer rax)
            (Sub r8 rax)
            (Mov rax r9)
            )]
    ['< 
      (seq  (Pop r8)
            (assert-integer r8)
            (assert-integer rax)
            (Cmp r8 rax)
            if-lt)]
    ['=
      (seq  (Pop r8)
            (assert-interger r8)
            (assert-integer rax)
            (Cmp r8 rax)
            if-equal)]
    )) 

(define if-equal
  (seq  (Mov rax  (value->bits #f))
        (Mov r9   (value->bits #t))
        (Cmove rax r9) 
        ))

;; 🆕
(define if-lt
  (seq  (Mov rax  (value-> bits #f))
        (Mov r9   (value-> bits #t))
        (Cmovl rax r9)
        ))


;; 🆕
(define pad-stack
  (seq  (Mov r15 rsp)
        (And r15 #b1000)
        (Sub rsp r15)))

;; 🆕
(define unpad-stack
  (seq  (Add rsp r15)))

(define assert-integer
    (assert-type mask-int type-int)) ;; this case, mask=1, type=0

(define assert-char ;; understand the syntax
    (assert-type mask-char type-char))

(define (assert-type mask type)
  (lambda (arg) ;; rax is passed as arg
    (seq  (Mov r9 arg)
          (And r9 mask)
          (Cmp r9 type) ;; if r9=0, then it's integer
          (Jne 'err)))) ;; ❌ not int, jmp to label error (which calls an external error function)

(define assert-byte
  (seq  (assert-integer rax)
        (Cmp rax (value->bits 0))
        (Jl 'err)
        (Cmp rax (value->bits 255))
        (Jg 'err)
  ))


;; codepoint from interpreter but in low level
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
(current-objs '("runtime.o"))

(asm-interp (compile (parse '(+ 10 20))))
-> 60

(bits->value (asm-interp (compile (parse '(+ 10 20)))))
-> 30

(asm-interp (compile-e (parse '(+ 42 (let ((x 10)) x))) '() ))
-> 104

(bits->value (asm-interp (compile-e (parse '(+ 42 (let ((x 10)) x))) '() )))
-> 52
```
