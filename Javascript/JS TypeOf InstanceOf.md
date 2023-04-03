# JS Typeof - Instanceof

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-04-03

---

# 🎬 Intro 
`typeof` and `instanceof` are both operators in JavaScript that are used to check the type of a value or an object. However, they work differently and have different use cases.

[[JS Operators|See More Operators]]

# The Type-Of Operator

`typeof`
- Returns a string indicating the type of an operand.

```js
typeof "Hello World" // returns "string"
typeof 42 // returns "number"
typeof true // returns "boolean"
typeof undefined // returns "undefined"
typeof null // returns "object"
typeof [1, 2, 3] // returns "object"
typeof { name: "John", age: 30 } // returns "object"
```

**Note**:
- `typeof null` returns `"object"`, which is a known quirk of JavaScript. This is because `null` is considered an empty object reference in JavaScript.


# The Instance-Of Operator

`instanceof`
- Checks if an object is an instance of a particular class.
```js
var today = new Date();
today instanceof Date // returns true
today instanceof Object // returns true

var names = ["John", "Paul", "George", "Ringo"];
names instanceof Array // returns true
names instanceof Object // returns true

var person = { name: "John", age: 30 };
person instanceof Object // returns true
person instanceof Array // returns false

```

In the above example,
- `today` is an instance of the `Date` class, 
- `names` is an instance of the `Array` class, and 
- `person` is an instance of the `Object` class.

# Summary
In summary, `typeof` checks the data type of a value or variable, while `instanceof` checks if an object is an instance of a particular class.