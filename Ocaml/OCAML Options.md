# 🐫 OCAML Options

📚Class: CMSC 330 Organization of Programming Languages 

📓Subject: OCAML 

✏️Section: 0105 

📅Date: 2023-03-07


---

# 🎬 Intro to Options

An `option` type is a built in variant that indicates the presence or absence of a value of type `'a`:
```ocaml
type 'a option = 
| None
| Some of 'a
```

