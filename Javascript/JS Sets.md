# JS Sets

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-04-02

---

# 🎬 Intro to Sets

Set is a built-in object that represents a collection of unique values, where duplicates are not allowed. 

A Set can store any type of value, including objects, and provides methods to add, remove, and check if a value exists in the set.

## Declaring and Initializing

```js
const mySet = new Set();
```

## Adding Values to a Set
```js
mySet.add(1);
mySet.add('two'); 
mySet.add(true);
```

## Removing Values from a Set
```js
mySet.delete(2);
// Output: {1, "two"}
```

## Check Size of a Set
```js
console.log(mySet.size);
// Output: 2
```

## Check Value Exists in  a Set
```js
console.log(mySet.has(1)); // Output: true 
console.log(mySet.has('three')); // Output: false
```

## Loop Over a Set
```js
mySet.forEach( (value) => { console.log(value); } );
// 1
// "two"

for (let value of mySet) { // for...of since Set is an iterable object
    console.log(value));
}
// 1
// "two"
```

## Clear
```js
mySet.clear()
// Sets = {}
```

## Creating a Set from an Array
```js
let setFromArray = new Set(arr);
```