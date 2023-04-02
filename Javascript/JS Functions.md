#  JS Functions

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 0101

🗓️Date: 2023-03-05

---

# ✅ Useful Functions

## `map()`
- Allows you to loop over an array's elements,
- Modifies each element by executing a function on each element. 
- **Note**: `.map()` returns a new array
```javascript
newarr = [1,2,3,4].map(num => num * 2)
// => [2,4,6,8]
```

```js
newarr = [1,2,3,4].map(num => num * 2)
// => [2,4,6,8]
```

> [!NOTE]- Title
> ```python
>print(A.length)
> ```


## `join()`
- Join each element of the array with the passed value
- Returns a **String**
```javascript
[1,2,3,4].join("-")
// => "1-2-3-4"
```

## `every()`
- Checks if all elements in an array passes a given test function
- `every()` returns True if **ALL** passes; otherwise, False (search stops)
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
- Returns True if **ONE** passes (search stops); otherwise, False
- The `some()` function takes one argument
	- a compare function (or lambda), that gives a condition to be met
	- If the condition returns **True**, the loop stops and the `some()` returns **True**.

```javascript
// Check for odd in array
[2, 6, 8, 1, 4].some( elem => elem%2 == 1)
// Loop1 elem: 2
// Loop2 elem: 6  
// Loop3 elem: 8
// Loop4 elem: 1 , returns True , end loop
```

## `sort()`
- Sorts an array in ascending or descending order.
- Note: `.sort()` modifies the original array
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

**Example**:
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
- You can destructure by passing in `(element, index)` as parameters
**Rule**:
- The `forEach` function takes one argument
	- a callback function that do something to each element in the array.

**Example**:
```javascript
const numbers = [1, 2, 3, 4, 5]; 
numbers.forEach(function(number) { 
    document.writeln(`Elem: ${elem}`)
});
// [2, 3, 4, 5, 6]

numbers.forEach( (elem, idx) => 
    document.writeln(`Index: ${idx}, Elem: ${elem}`);
)
```

## `localeCompare()`
- Compares two strings and return 
> [!info] Rule
> ```js
> x.localeCompary(y)


> [!todo] Return
> -  1 if `x` < `y`
> - 0 if `x` = `y`
> - 1 if `x` > `y`


> [!example] Example
> ```js
> "Rose".localeCompare("Kathy") // x > y => 1
"Bob".localeCompare("Kathy")  // x < y => -1
"Kathy".localeCompare("Kathy") // => 1



## `filter()`
- Creates a **new array** by filtering out elements based on a given condition. 

**Rule**: 
- The `filter()` function takes one argument
	- a callback function (or lambda), which is executed for each element in the array
- Returns a **new array** with elements that **passed** the given condition.

**Example**:
```javascript
const numbers = [1, 2, 3, 4, 5, 6]; 

const evenNumbers = numbers.filter( (number) =>  
    number % 2 === 0; 
);
// => [2, 4, 6]
```


## `getAttribute()` - `setAttribute()`
- We can get the attribute of any HTML element
```javascript
document.querySelector("#theImage").getAttribute("src")
// => images/Testudo01.jpg

document.querySelector("#theImage").setAttribute("src", "images/Testudo02.jpg")
```


## `setTimeout` vs `clearInterval` vs `setInterval`
- `setTimeout` - delays the execution of a function
	- Takes a function for execution
	- Takes an integer for delay
```js
const delayInMilliSeconds = 4000;
setTimeout("message()", delayInMilliSeconds);
```

- `setInterval`: runs the code every `intervalInMiliseconds`
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

# 🤷🏻‍♂️ How to

## Default Parameters
```javascript
function task(name = "John", age = 21, salary = special()) {
    document.writeln(name + ' ' + age + ' ' + salary + "<br>");
}
function special() { return 10000;}
```

## Random RGB Color
```js
function getRandomColor() { 
	const r = Math.floor(Math.random() * 256); // 0 (inclusive) to 256 (exclusive)
	const g = Math.floor(Math.random() * 256); 
	const b = Math.floor(Math.random() * 256);
	const alpha = Math.random().toFixed(1);
	
	return `rgba(${r}, ${g}, ${b}, ${alpha})`; }
```
- Set a random color to an element
```js
const element = document.getElementById("my-element"); element.style.backgroundColor = getRandomColor();
```




## Replace Class with `classList`

```javascript
function replaceClass() { 
  var element = document.getElementById("my-paragraph");
  element.classList.replace("red", "blue"); 
}
```
