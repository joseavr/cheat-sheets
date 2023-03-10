# OCAML Options
Class: [[OCAML]]
Subject: #
Date: 2023-03-07
Topics: #, #, # 

---

# 🎬 Intro to Options

An `option` type is a built in variant that indicates the presence or absence of a value of type `'a`:
```ocaml
type 'a option = 
| None
| Some of 'a
```

