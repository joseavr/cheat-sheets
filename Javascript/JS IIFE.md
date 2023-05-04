# JS Immediately Invoked Function Expression (IIFE)

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-04-02

---
# 🎬 Intro to IIFE

- IIFE: call a function immediately
- Does not have a name, and it is self-executing
- Two parts  
	- Anonymous function enclosed in a scope `()`
	- Another `()`, after the enclosed scope, to call the lambda function

**Notes**:
- IIFE - Prevents accessing variables within the IIFE idiom as well as polluting the global scope
- Emulates block-scoped variables
- Not needed if “let” is used instead of “var”

```js
// Call a lambda function without assigning to a variable
( 
    () => {
    var hiddenStar = "HiddenStar";
    document.writeln("within the IIFE");} 
)()
```