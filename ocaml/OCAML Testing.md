# OCAML Testing

📚Class: CMSC 330 Organization of Programming Languages 

📓Subject: OCAML 

✏️Section: 0105 

📅Date: 2023-03-07


---

# 🐫 Use Ocaml Extension
- See real time errors with
	- OCAML extension
	- Error Lens extension

# 📝 Testing PublicTests
## Compile Test
- It generates a folder `_build`
```shell
dune build test/public/public.exe
```

## List Tests
```shell
_build/default/test/public/public.exe -list-test
```

## Run Specific Test
```shell
_build/default/test/public/public.exe -only-test public:#
```



# 📝 Test Code in Interactive Shell (UTOP)
```
# with ocaml extension (recommended)
Select code
Shift + Enter
```
or follow nex steps
```shell
dune utop src
```

## 1. Load Function definitions in UTOP
```utop
open Basics;;
```

## Show these definitions (optional)
```utop
show rev_tup;;
```

## 2. Test function in UTOP
```utop
rev_utop (3;4;5);;

=> int * int = (5;4;3)
```


# 😖 Other Testing (no recommended)
## Test Locally
```shell
dune runtest -f
```

## Test Specific File
```
dune runtest test/student
```
