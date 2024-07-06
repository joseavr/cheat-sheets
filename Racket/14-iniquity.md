# Iniquity: function definitions and calls

In the previous programs, we implemented data structures like vector, box, strings., and used operations on them but they were fix size.  

How about any size? For this we will need recursion. For example:

```racket
(len (cons 10 (cons 20 (cons 30 '()))))
```

In iniquity, we will add recursive function.



## AST
```racket
#lang racket
(provide Lit Prim0 Prim1 Prim2 Prim3 If Eof Begin
         Let Var Prog Defn App)

(struct Prog (ds e) #:prefab) ;; 🆕

(struct Defn (f xs e) #:prefab) ;; 🆕

(struct Eof () #:prefab)
(struct Lit (d) #:prefab)
(struct Prim0 (p) #:prefab)
(struct Prim1 (p e) #:prefab)
(struct Prim2 (p e1 e2)  #:prefab)
(struct Prim3 (p e1 e2 e3)  #:prefab)
(struct If (e1 e2 e3) #:prefab)
(struct Begin (e1 e2) #:prefab)
(struct Let (x e1 e2) #:prefab)
(struct Var (x) #:prefab)
(struct App (f es) #:prefab) ;; 🆕
```

## The `and` in match

It is like `&&` in js but also binds to the variable.

```racket
(match 100
  [(and x 100 y) 1]  
  [_ 2])
-> 1 ; (and x 100 y) is true then return 1

(match 100
  [(and x 100 y) x]  
  [_ 2])
-> 100 ; because x = 100

(match 100
  [(and x 100 y) y]  
  [_ 2])
-> 100 ; because y = 100

(match 100
  [(and x 101 y) y]  
  [_ 2])
-> 2 ; because did not match 101
```

## The `apply`

Takes a function and applies args as list 

```racket
(define (f x y) (+ x y))
(apply f' '(50 100)) ;; args[0]=50 and args[1]=100 to f'
-> 150

(apply + '(1 2 3))  ;; args[0]=1, args[1]=2, args[2]=3
-> 6
```

## The '.' arguments

The `.` means takes all arguments as a list `s`

```racket
(define (f . s) s)

(f 1 2 3)
-> '(1 2 3)
```

## Parse

We will be using the `Program` struct and `App` struct, so that the program can receive as many arguments that consists of multiple `define`'s an expressions. 

Parse now becomes a bit more complicated. 

```racket

;; 🆕
(define (parse . s)  
  (match s
    ;; suppose s matches to:
    ;; '( (define (f x) x)
    ;;    (define (g x) x)  
    ;;     (f 10) )
    [(cons (and (cons 'define _) d) s) ;; match 1st Define as `d` and the rest as `s`
    ;; d = '(define (f x) x)
    ;; s = '((define (g x) x) (f 10))
     (match (apply parse s) ; recursively call parse till last term '(f 10) -> (Prog '() parsed-f)
       [(Prog ds e)         ; match this (Prog '() ...) and recursively populate empty list '().
        (Prog (cons (parse-define d) ds) e)])]
    [(cons e '()) (Prog '() (parse-e e))]
    [_ (error "program parse error")]))

;; 🆕 Parse a single Define
(define (parse-define s)
  (match s
    [(list 'define (list-rest (? symbol? f) xs) e)
     (if (andmap symbol? xs)
         (Defn f xs (parse-e e))
         (error "parse definition error"))]
    [_ (error "Parse defn error" s)]))

(define (parse-e s)
  (match s
    [(? datum?)               (Lit s)]
    ['eof                     (Eof)]
    [(? symbol?)              (Var s)]
    [(list 'quote (list))     (Lit '())]
    [(list (? op0? p0))       (Prim0 p0)]
    [(list (? op1? p1) e)     (Prim1 p1 (parse-e e))]
    [(list (? op2? p2) e1 e2) (Prim2 p2 (parse-e e1) (parse-e e2))]
    [(list (? op3? p3) e1 e2 e3)
     (Prim3 p3 (parse-e e1) (parse-e e2) (parse-e e3))]
    [(list 'begin e1 e2)
     (Begin (parse-e e1) (parse-e e2))]
    [(list 'if e1 e2 e3)
     (If (parse-e e1) (parse-e e2) (parse-e e3))]
    [(list 'let (list (list (? symbol? x) e1)) e2)
     (Let x (parse-e e1) (parse-e e2))]
    ;; 🆕
    [(cons (? symbol? f) es)  
     (App f (map parse-e es))]

    [_ (error "Parse error" s)]))



(define (datum? x)
  (or (exact-integer? x)
      (boolean? x)
      (char? x)
      (string? x)))

(define (op0? x)
  (memq x '(read-byte peek-byte void)))

(define (op1? x)
  (memq x '(add1 sub1 zero? char? integer->char char->integer
                 write-byte eof-object?
                 box unbox empty? cons? box? car cdr
                 vector? vector-length string? string-length)))

(define (op2? x)
  (memq x '(+ - < = eq? cons
              make-vector vector-ref make-string string-ref)))

(define (op3? x)
  (memq x '(vector-set!)))
```


## Interpreter
```racket
;; interp.rkt

;; 🆕
(define (interp p)
  (match p
    [(Prog ds e) ;; Initially, matches to `Prog`
     (interp-env e '() ds)])) ;; besides the context environment '(), we also need the definitions `ds`

;; 🆕 New argument `ds` - definitions
(define (interp-env e r ds)
  (match e
    [(Lit d) d]
    [(Eof)   eof]
    [(Var x) (lookup r x)]
    [(Prim0 p) (interp-prim0 p)]
    [(Prim1 p e)
     (match (interp-env e r ds)
       ['err 'err]
       [v (interp-prim1 p v)])]
    [(Prim2 p e1 e2)
     (match (interp-env e1 r ds)
       ['err 'err]
       [v1 (match (interp-env e2 r ds)
             ['err 'err]
             [v2 (interp-prim2 p v1 v2)])])]
    [(Prim3 p e1 e2 e3)
     (match (interp-env e1 r ds)
       ['err 'err]
       [v1 (match (interp-env e2 r ds)
             ['err 'err]
             [v2 (match (interp-env e3 r ds)
                   ['err 'err]
                   [v3 (interp-prim3 p v1 v2 v3)])])])]
    [(If e0 e1 e2)
     (match (interp-env e0 r ds)
       ['err 'err]
       [v
        (if v
            (interp-env e1 r ds)
            (interp-env e2 r ds))])]
    [(Begin e1 e2)
     (match (interp-env e1 r ds)
       ['err 'err]
       [v    (interp-env e2 r ds)])]
    [(Let x e1 e2)
     (match (interp-env e1 r ds)
       ['err 'err]
       [v (interp-env e2 (ext r x v) ds)])]

    ;; 🆕 
    [(App f es)
     (match (interp-env* es r ds)
       ['err 'err]
       [vs
        (match (defns-lookup ds f)
          [(Defn f xs e)
           ; check arity matches
           (if (= (length xs) (length vs))
               (interp-env e (zip xs vs) ds)
               'err)])])]))  



(define (interp-env* es r ds) ;; 🆕 definitions `ds`
  (match es
    ['() '()]
    [(cons e es)
     (match (interp-env e r ds)
       ['err 'err]
       [v (match (interp-env* es r ds)
            ['err 'err]
            [vs (cons v vs)])])]))

;; 🆕 
(define (defns-lookup ds f) 
  (findf (match-lambda [(Defn g _ _) (eq? f g)])
         ds))

;; 🆕 creates a pair: ( (x0 y0) (x1 y2) ... )
(define (zip xs ys)
  (match* (xs ys)
    [('() '()) '()]
    [((cons x xs) (cons y ys))
     (cons (list x y)
           (zip xs ys))]))

(define (lookup r x)
  (match r
    [(cons (list y val) r)
     (if (symbol=? x y)
         val
         (lookup r x))]))

;; Env Id Value -> Env
(define (ext r x v)
  (cons (list x v) r))
```


Match Lambda is the same as:

```racket
(( lambda (id) 
    (match id 
      [10 #t] 
      [_ #f])) 10)
-> #t
```

There is no changes in Interp-prim.

## Compiler

```racket
;; compile.rkt

;; 🆕 Initially, matches to `Prog`
(define (compile p) ;;  program `p`
  (match p 
    [(Prog ds e)
      (prog
        (Global 'entry)
        (Extern 'peek_byte)
        (Extern 'read_byte)
        (Extern 'write_byte)
        (Extern 'raise_error)
        (Label 'entry)

        ;; <- stack is 8-byte aligned here

        ;; save callee-saved register
        (Push rbx)
        (Push r15) ;; stack 16-byte aligned ✅

        (Mov rbx rdi) ;; recv heap pointer
        
        (compile-e e '()) 

        ;; restore callee-save register
        (Pop r15)
        (Pop rbx)  
        (Ret)

        (compile-defines ds)   ;; 🆕

        ;; Error handler
        (Label 'err)
        pad-stack 
        (Call 'raise_error))]))

;; 🆕 compile lst of defines
(define (compile-defines ds)
  (match ds
    ['() (seq)]
    [(cons d ds)
     (seq (compile-define d)
          (compile-defines ds))]))

;; 🆕 compile single define
(define (compile-define d)
  (match d
    [(Defn f xs e)
     (seq (Label (symbol->label f))
          (compile-e e (reverse xs))
          (Add rsp (* 8 (length xs))) ; pop args
          (Ret))]))

(define (compile-e e c) 
  (match e
    [(Lit i)          (compile-value i)]
    [(Eof)            (compile-value eof)]
    [(Var x)          (compile-variable x c)]
    [(Prim0 p)        (compile-prim0 p)]
    [(Prim1 p e)      (compile-prim1 p e c)] 
    [(Prim2 p e1 e2)  (compile-prim2 p e1 e2 c)]
    [(If e0 e1 e2)    (compile-if e0 e1 e2 c)]
    [(If e0 e1 e2 e3)    (compile-if e0 e1 e2 e3 c)] 
    [(Begin e1 e2)    (compile-begin e1 e2 c)]
    [(Let x e1 e2)    (compile-let x e1 e2 c)]
    [(App f es)       (compile-app f es c)]     ;; 🆕
  ))

;; 🆕
(define (compile-app f es c)
  (let ((r (gensym 'ret)))
    (seq (Lea rax r)  ; get the return address
         (Push rax)   ; push the return address 
         (compile-es es (cons #f c))
         (Jmp (symbol->label f))
         (Label r))))

;; 🆕
(define (compile-es es c)
  (match es
    ['() '()]
    [(cons e es)
     (seq (compile-e e c)
          (Push rax)
          (compile-es es (cons #f c)))]))

(define (compile-value v)
  (cond [(string? v) (compile-string v)]  
        [else        (Mov rax (value->bits v))]))

;; lookup the environment and get the index i
;; store in rax the index position i from the stack
(define (compile-variable x c)
  (let ((i (lookup x c)))
        (seq (Mov rax (Offset rsp i)))
        ))

(define (compile-string s)
  (let ((len (string-length s)))
    (if (zero? len)
        (seq (Mov rax type-str))
        (seq (Mov rax len)
             (Mov (Offset rbx 0) rax)
             (compile-string-chars (string->list s) 8)
             (Mov rax rbx)
             (Or rax type-str)
             (Add rbx
                  (+ 8 (* 4 (if (odd? len) (add1 len) len))))))))

(define (compile-string-chars cs i)
  (match cs
    ['() (seq)]
    [(cons c cs)
     (seq (Mov rax (char->integer c))
          (Mov (Offset rbx i) 'eax)
          (compile-string-chars cs (+ 4 i)))]))


(define (compile-prim0 p)
  (compile-op0 p))


(define (compile-prim1 p e c) 
  (seq
    (compile-e e c)
    (compile-op1 p)))

(define (compile-prim2 p e1 e2 c)
  (seq
    (compile-e e1 c)
    (Push rax) ;; since e1 and e2 evaluated needs rax, we push the first to stack to keep track
    (compile-e e2 (const (gensym) c)) ;; e2 evualted stored in rax
    (compile-op2 p))) ;; call operant, i.e +, takes both args1 (in stack) and arg2 (in rax)


(define (compile-prim3 p e1 e2 e3 c)
  (seq (compile-e e1 c)
       (Push rax)
       (compile-e e2 (cons #f c))
       (Push rax)
       (compile-e e3 (cons #f (cons #f c)))
       (compile-op3 p)));; Expr Expr Expr CEnv -> Asm

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


(define (compile-begin e1 e2 c)
  (seq  (compile-e e1 c)
        (compile-e e2 c)))

(define (compile-let x e1 e2 c)
  (seq  (compile-e e1 c) ;; let x = 10 + 20
        (Push rax)       ;; push 30 (we need value later)
        (compile-e e2 (cons x c))
        (Add rsp 8) ;; we could (Pop rax) but we dont want to replace rax
  ))


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

Some testing:

```racket
(compile (parse '(define (f x y) x) '(f 1 2) ))
```
