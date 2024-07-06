# Knock

The Knock program adds matching features. 

## AST

```racket
#lang racket
(provide Lit Prim0 Prim1 Prim2 Prim3 If Eof Begin
         Let Var Prog Defn App)

(struct Prog (ds e) #:prefab)
(struct Defn (f xs e) #:prefab)

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
(struct App (f es) #:prefab)

(struct Match (e ps es) #:prefab)  ;; 🆕
(struct Box (p) #:prefab)          ;; 🆕
```

## Parse

```racket

(define (parse . s)
  (match s
    [(cons (and (cons 'define _) d) s)
     (match (apply parse s)
       [(Prog ds e)
        (Prog (cons (parse-define d) ds) e)])]
    [(cons e '()) (Prog '() (parse-e e))]
    [_ (error "program parse error")]))

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
    [(cons 'match (cons e ms))
     (parse-match (parse-e e) ms)]

    [(cons (? symbol? f) es)
     (App f (map parse-e es))]
    [_ (error "Parse error" s)]))    


;; 🆕 Expr [Listof S-Expr]
(define (parse-match e ms)
  (match ms
    ['() (Match e '() '())]
    [(cons (list p r) ms)
     (match (parse-match e ms)
       [(Match e ps es)
        (Match e
               (cons (parse-pat p) ps)
               (cons (parse-e r) es))])]
    [_ (error "Parse match error" e ms)]))

;; 🆕 S-Expr -> Pat
(define (parse-pat p) ;; parse patterns
  (match p
    [(? datum?) (Lit p)]
    [(? symbol?) (Var p)]             ;; parses symbols, i.e match against wild-card "_" in a match condition
    [(list 'quote (list)) (Lit '())]  ;; match against '()
    [(list 'box p)                    ;; match against (box ...)
     (Box (parse-pat p))]
    [(list 'cons p1 p2)               ;; match against (cons ...)
     (Cons (parse-pat p1) (parse-pat p2))]
    [(list 'and p1 p2)                ;; match again (and ...)
     (Conj (parse-pat p1) (parse-pat p2))]))

...
```

Let's test

```racket
(parse-e '(match (add1 42) [x (+ x x)]))
-> '#s(Match #s(Prim1 add1 #s(lit 42)) (#t) (#s(Prim2 + #s(Var x) #s (Var x))))

(parse-e '(match 10 [10 1]))
-> '#s(Match #s(Lit 10) (#s(Lit 10)) (#s(Lit 1)))

(parse-e '(match 99 [10 1] [99 2] [100 3]))
-> '#s(Match #s(Lit 99) (#s(Lit 10) #s(Lit 99) #s(Lit 100)) 
                        (#s(Lit 1) #s(Lit 2) #s(Lit 3)))

(parse-e '(match 10 [_ 1])) ;; wild card
-> '#s(Match #s())                        
```

## Interpreter

```racket
(define (interp p)
  (match p
    [(Prog ds e)
     (interp-env e '() ds)]))

;; Expr Env -> Answer
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
    [(App f es)
     (match (interp-env* es r ds)
       ['err 'err]
       [vs
        (match (defns-lookup ds f)
          [(Defn f xs e)
           ; check arity matches
           (if (= (length xs) (length vs))
               (interp-env e (zip xs vs) ds)
               'err)])])]               
    ;; 🆕
    [(Match e ps es)
     (match (interp-env e r ds)
       ['err 'err]
       [v   (interp-match v ps es r ds)])]))       


(define (interp-env* es r ds)
  (match es
    ['() '()]
    [(cons e es)
     (match (interp-env e r ds)
       ['err 'err]
       [v (match (interp-env* es r ds)
            ['err 'err]
            [vs (cons v vs)])])]))

;; 🆕 Value [Listof Patterns] [Listof Expr] Env Defns -> Answer
(define (interp-match v ps es r ds)
  (match* (ps es)
    [('() '()) 'err]
    [((cons p ps) (cons e es))
     
     (match (interp-match-pat p v r)
       [#f (interp-match v ps es r ds)]
       [r2  (interp-env e r2 ds)])]))
;; example:
     ;; (match 10 [x (add1 x)]) 
     ;; interp-match-pat (Var x) 10 '()
     ;; r2=(x 10) then (add1 x)


;; 🆕 Pat Value Env -> [Maybe Env]
(define (interp-match-pat p v r)
  (match p
    [(Var '_) r]   ;; match any variable i.e (Var 'x)
    [(Var x) (ext r x v)] ;; match any value
    [(Lit l) (and (eqv? l v) r)]
    [(Box p)
     (match v
       [(box v)
        (interp-match-pat p v r)]
       [_ #f])]
    [(Cons p1 p2)
     (match v
       [(cons v1 v2)
        (match (interp-match-pat p1 v1 r)
          [#f #f]
          [r1 (interp-match-pat p2 v2 r1)])]
       [_ #f])]
    [(Conj p1 p2)
     (match (interp-match-pat p1 v r)
       [#f #f]
       [r1 (interp-match-pat p2 v r1)])]))
;; some exmaples:
;; (interp-match-pat (Lit 100) 99 '((y 100))) -> #f
;; (interp-match-pat (Lit 99) 99 '((y 100)))  -> '((y 100))


...  
```

## Compiler 

```racket

```