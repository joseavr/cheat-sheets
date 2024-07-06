# Untitled

📚Class:

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section:

🗓️Date: 2024-05-31

---

# Useful Commands

Test a Racket file.

```bash
raco test path/to/the/file.rkt

```

---

Since my OS is macOS, we need `arch -x86_64` before `gcc`

Use gcc compiler to compile C program (in arm chip macOS) to a binary (lowest level) -> main.o (object file)

```bash
arch -x86_64 gcc -c main.c
```

See binary to human readable assembly code -> `main.o`

```bash
objdump -Sd main.o
```

Link two object files together -> executable `a.out`

```bash
arch -x86_64 gcc main.o entry.o
./a.out   // run program
```

---

Compile x86 assembly code to object file -> `entry.o`.

```bash
nasm -f macho64 -o entry.o entry.s
```

---

Save Racket assembly code (a86) to assembly file (x86) -> `t.s`
Compile x86 to object file -> `t.o`
Link objects to create executable -> `a.out`
Run program

```bash
racket entry.rkt > t.s
nasm -f macho64 -o t.o t.s
arch -x86_64 gcc main.o t.o
./a.out
```
