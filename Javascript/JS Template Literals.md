# JS Template Literals

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 0101

🗓️Date: 2023-02-22

---

# 🎬 Intro 
Template literals, also known as template strings, are a feature in JavaScript that allows for the embedding of expressions inside of string literals. 

Template literals are defined using backticks `` ` ` `` instead of single or double quotes.

# 📏 Rule
```js
str = `string text ${expression} string text`
```

#  🔭 Example
```javascript
const date = new Date();
const dateString = `Today is ${date.toDateString()}`;
console.log(dateString); // output: Today is Sun Feb 28 2023
```

# 🛸 Multi Line Strings
```js
const multilineString = `This is a
multiline
string`;
console.log(multilineString); // output: This is a
                               //         multiline
                               //         string
```

