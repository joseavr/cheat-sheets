# OCAML Review

📚Class: CMSC 330 Organization of Programming Languages 

📓Subject: OCAML 

✏️Section: 0105 

🗓️Date: 2023-04-18

---

# Review

- Lexing: Scanning/TOkenizing
	- Create token, convert sentences to a list tokens, tokens are the basis of the language, common tokens tell us smth each word, 
	- could be PART OF SPEECH, like blue, angry, etc
	- describing sets of colection of words
	- what else do besides converting to tokens?
		- each word is a valid word, 
		- make sure every word is part of the lexicon
		- Gol: translate one language to another, like spanish to english , but also to programming languages like, Rust to C, C to Java, etc
		- 
	- In brief, what lexicon does? converts to string to tokens and checks if words are in lexicon
- Parsing:
	- What is the goal? takes some sort of token list and returns an AST (abstract syntax tree) 
	- AST: represents the grammar of the language
- Generator -> relates the sentences of a language
- "evaluator" -> figuring out the meaning of the input
- With all these 4 things, interpreter or compiler? 
	- compiler: translates whole language to another language
	- interpreter: gives you an value from a input


- CFG -> a set of strings