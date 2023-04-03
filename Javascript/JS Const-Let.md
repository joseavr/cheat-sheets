# JS Const vs Let

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 0101

🗓️Date: 2023-04-02

---

# The Difference

In JavaScript, `const` and `let` are used to declare variables, but there are differences between the two:

1.  `const` - short for "constant" - declares a variable that cannot be reassigned a new value. This means that the variable is read-only once it is initialized.
```js
const PI = 3.14159;
PI = 3; // This will throw an error because PI is a constant and cannot be reassigned a new value.

```

2.  `let` declares a variable that can be reassigned a new value.
```js
let x = 5;
x = 10; 
// This is valid because x is a variable declared with let and can be reassigned a new value.
```

**Note**:
- Good practice to use `const` when you have a variable that should not be changed, and 
- `let` when you have a variable that needs to be reassigned a new value. 
- Additionally, using `const` can help prevent bugs in your code by ensuring that variables are not unintentionally changed.