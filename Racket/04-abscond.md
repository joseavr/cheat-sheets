📚Class:

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section:

🗓️Date: 2024-05-30

---

# Abscond

Overview: We will write a simple compiler that takes racket code -> parses it to build an AST -> use AST to compiler to another language

**Note:** we use the compiler to compile to another language (this case a86) & interpreter to check the compiler is outputing the right thing (since this is a compiler class we can omit interpreter but it is a good practice for reinforcing, normally interpreter is given)

What is Abscond? A simple program that only takes integer literals.

## Simple AST

This is the struct for the AST

```racket
; ast.rkt

#lang racket
(provide Lit)

(struct Lit (i) #:prefab)
; prefab adds .toString() when invoking this AST

```

## Simple Parser

It parses only integers

```racket
; parser.rkt

#lang racket
(provide parse)
(require "ast.rkt")

(define (parse s)
  (match s
  [(? exact-integer?) (Lit s)]
  [_ (error "Parse error")]
))
```

If we run this:

```racket
(parse 1)
-> '#s(Lit 1)'

(parse 2)
-> Parse error
```

## Simple Interpreter

1. Interpreter will take the parsed as input
2. Matches and outputs a value (given by the interpreter).

```racket
; interp.rkt

#lang racket
(provide interp)
(require "ast.rkt")

;; Expr -> Integer
(define (interp e)
  (match e
  [(Lit i) i]
  [_ (error "interp erorr")]
))
```

If we run the this:

```racket
(interp (parse 10))
(interp '(Lit 10))
-> 10
```

## Simple Compiler

What the compiler does?

1. The compiler will take the parsed as input
2. Matches the input and outputs to the target language (this case a86)

**Note:** We will use racket to output in a86 (assembly) since racket supports it

**Note:** This compiled a86 code, turns out that can be also linked and used along with C code/program.

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
    [(Lit i) (Mov 'rax i)]))
```

If we run this:

```racket
(compile (parse 42))
-> (list (Global 'entry) (Label 'entry) (Mov 'rax 42) (Ret))
```

now with asm-interp from a86 package imported:
```racket
(asm-interp (compile (parse 42)))
-> 42
```

**Note:** asm-interp runs the executable from the compiled file. Not the interpreter (interp just receives directly code)

