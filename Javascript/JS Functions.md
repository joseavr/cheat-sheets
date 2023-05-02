#  JS Functions

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-03-05

---

# ✅ Useful Array Functions

## `reduce()`
- Same as `fold_left` in OCAML
- It takes a callback function as its first argument, which is applied to each element of the array and accumulates a single result.
- The `reduce()` takes two arguments
	- a callback function, which takes two arguments
		- `acc` - accumulates at each iteration.
		- `e` - current element being processed.
		- `idx` 
		- `arr` 
	- an initial value for the `accumulator` - if not given, acc = A[0] and loop starts at A[1]
- **Note**: needs a `return` so `accumulator` is updated for the next iteration
```js
// RULE
arr.reduce( (acc, e) => do_smth(acc,e) , initial_acc )

// EXAMPLE
const sum = [1, 2, 3, 4, 5].reduce( (accumulator, eachElement) => {
  return accumulator + eachElement; // accumulator = accumulator + eachElement
}, 0);
// Output: 15
```

---

## `filter()`
- Filters out elements based on a given condition. 
- The `filter()` function takes one argument
	- a callback function (or lambda), which is executed for each element in the array
	- Callback function accepts destructuring
		- `elem`
		- `idx`
		- `arr`
- **Note**: returns a **NEW ARRAY**

```javascript
const numbers = [1, 2, 3, 4, 5, 6]; 

const evenNumbers = numbers.filter( (number) =>  
    number % 2 === 0; 
);
// => [2, 4, 6]
```


## `map()`
- Same `map` as OCAML
- Modifies each element based on a function passed. 
- The `map()` takes one argument
	- callback function (or lambda) accepts destructuring
		- `elem` - for modifying it
		- `idx` 
		- `arr`
- **Note**: returns a **NEW ARRAY** 
```javascript
newarr = [1,2,3,4].map( (elem,idx,arr) => elem * 2)
// => [2,4,6,8]
```

---

## `join()`
- Join each element of the array with the passed value
- Returns a **STRING**
```javascript
[1,2,3,4].join("-")
// => "1-2-3-4"
```

## `every()`
- Checks if all elements in an array passes a given test function
- Callback function (or lambda) accepts destructuring
	- `elem` 
	- `idx` 
	- `arr`
- Returns True if **ALL** passes; otherwise, False (search stops)
```javascript
// Check for odd in array
[2, 6, 8, 1, 4].every( elem => elem%2 == 1)
// Loop1 elem: 2 , False, end loop, returns False

[1, 3, 5, 7].every(elem => elem%2 == 1)
// Loop1 elem:1, True
// Loop2 elem:3, True
// Loop3 elem:5, True
// Loop4 elem:7, True
// => end loop, returns True
```

## `some()`
- Checks if at least one element in an array passes a given test function
- The `some()` function takes one argument
	- a compare function (or lambda), that gives a condition to be met
	- If the condition returns **True**, the loop stops and the `some()` returns **True**.
- Returns True if at least **ONE** passes (search stops); otherwise, False
```javascript
// Check for odd in array
[2, 6, 8, 1, 4].some( elem => elem%2 == 1)
// Loop1 elem: 2
// Loop2 elem: 6  
// Loop3 elem: 8
// Loop4 elem: 1 , returns True , end loop
```

## `localeCompare()`
- Compares two strings 
- Returns
	- -1 if `x` < `y`
	- 0 if `x` = `y`
	- 1 if `x` > `y`

```js
// Rule
x.localeCompary(y)

"Rose".localeCompare("Kathy") // x > y => 1
"Bob".localeCompare("Kathy")  // x < y => -1
"Kathy".localeCompare("Kathy") // => 0
```

--- 

## `sort()`
- Sorts an array in ascending or descending order.
- Note: **MODIFIES** the original array
```javascript
const fruits = ['banana', 'apple', 'orange', 'grape'];
fruits.sort();
// Output: ['apple', 'banana', 'grape', 'orange']
```

**Rule**:
- The `sort()` function takes one argument
	- a compare function (or lambda) that compares the elements of the array
-   If `compareFunction(a, b)` returns `-1`, `a` comes before `b`. **NO SWAP**
-   If `compareFunction(a, b)` returns `1`, `b` comes before `a`. **SWAP**
-   If `compareFunction(a, b)` returns `0`, **NO SWAP**
```javascript
// Reverse sort
const fruits = ['banana', 'apple', 'orange', 'grape'];

fruits.sort(compareFunction(a, b) {
  if (a > b) {
    return -1; // NO SWAP
  } else if (a < b) {
    return 1; // SWAP
  } else {
    return 0;
  }
});
// Output: ['orange', 'grape', 'banana', 'apple']
```


## `forEach()`
- Allows you to loop over an array's elements and execute a function on each element. 
- The `forEach` function takes one argument
	- a callback function that do something to each element in the array.
	- callback function (or lambda) accepts destructuring
		- `elem`
		- `idx` 
		- `arr`
```javascript
const numbers = [1, 2, 3, 4, 5]; 
numbers.forEach(function(number) { 
    document.writeln(`Elem: ${elem}`)
});
// [2, 3, 4, 5, 6]

numbers.forEach( (elem, idx, arr) => 
    document.writeln(`${idx}, ${elem}, ${arr}`);
)
```


## `find()`
- Find the first occurrence of a given function condition
- Returns the first `element` found
```js
fruits = ["apple", "pear", "banana", "orange", "plum", "grape"]
fruit = fruits.find( elem => elem.length >= 6 )
// fruit = banana
```


## `findIndex()`
- Same as `find()`
- Returns the first `index` found
```js
fruits = ["apple", "pear", "banana", "orange", "plum", "grape"]
fruit_idx = fruits.find( elem => elem.length >= 6 )
// fruit_idx = 2
```


---


## `setTimeout` vs `clearInterval` vs `setInterval`
- `setTimeout` - delays the execution of a function
	- Takes a function for execution
	- Takes an integer for delay
```js
const delayInMilliSeconds = 4000;
setTimeout("message()", delayInMilliSeconds);
```

- `setInterval` - runs the code every `intervalInMiliseconds`
	- returns an ID that `clearInterval` uses to stop execution
```js
const intervalInMilliseconds = 1000;
idGlobal = setInterval("swapImages()", intervalInMilliseconds); // Runs swapImages() every 1s

function swapImages() {
	let imageElement = document.querySelector("#myImage");
	let currentImage = imageElement.src, nextImage;
	if (currentImage.includes("Testudo1.jpg")) {
		nextImage = "images/Testudo2.jpg";
	} else if (currentImage.includes("images/Testudo2.jpg")){
		nextImage = "images/Testudo3.jpg";
	} else {
		nextImage = "images/Testudo1.jpg";
	}
	imageElement.src = nextImage; // takes 1000ms to load img
}

function stopAnimation() {   // this can be linked to a button to stop interval
	clearInterval(idGlobal);
	alert("Animation Stopped");
}
```


# Default Parameters
```javascript
function task(name = "John", age = 21, salary = special()) {
    document.writeln(name + ' ' + age + ' ' + salary + "<br>");
}
function special() { return 10000;}
```

# Arguments of a Function 
```js
function process(start, end, delta, message) {
	const args = arguments.length
	// => 4
	
	const last_arg = arguments[arguments.length - 1])
	// => message

	for (let val of arguments) {
		document.writeln(`${val}`);
	}
	// => start, end, delta, message
}
```

# [[JS Operators]]
