# JS For In vs For Of

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-04-02

---

# 🆚 `for...in` vs `for...of`

In JavaScript, the `for...in` and `for...of` loops are used for iterating over collections, but they work differently.

## `for...in`
- The `for...in` loop iterates over the **properties** of an object. 
- Works on all enumerable properties, including those inherited from the object's prototype chain.
- Used for iterating over the **keys** or **property names** of an object.

```js
const myObj = {a: 1, b: 2, c: 3};  

for (let prop in myObj) {   
    console.log(prop + ': ' + myObj[prop]); 
}
// a: 1 
// b: 2 
// c: 3
```


## `for...of`
- The `for...of` loop is used for iterating over **iterable objects** like arrays, strings, maps, sets, etc. 
- Iterates over the values of the iterable objects and NOT the properties.

```js
const myArr = [1, 2, 3];  
for (let val of myArr) {   
    console.log(val); 
}
// 1
// 2
// 3
```

## Summary 
- `for...in` is used for iterating over the properties of an object
- `for...of` is used for iterating over the values of an iterable object.


# 🙋‍♂️ What If

If you try to use the `for...of` loop on the `myObj` object in the example given, you will get a `TypeError` because `myObj` is not an iterable object. 

The `for...of` loop works only on iterable objects like arrays, strings, maps, sets, etc.

```js
const myObj = {a: 1, b: 2, c: 3};  
for (let val of myObj) {
    console.log(val); 
}
// `Uncaught TypeError: myObj is not iterable`
```
