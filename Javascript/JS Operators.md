# JS Operators

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-03-29

---

# 🎬 Intro to Operators
- Special keywords/shortcuts that are useful for specific scenarios 

# 1️⃣ Rest Operator
- Stores the remaining arguments as an array

## Functions
```js
function partyInfo(name, director, ...others) {
	// whenever seen ...<variable> is an ARRAY
	let arr;
	for (let each of others) {
		arr.push(each);
	}
	return arr;
}

partyInfo("FirstParty", "Ali", "Theresa", "Arushi");
// => ["Theresa", "Arushi"];
```

# 2️⃣ Spread Operator
- Allows to expand (**extracts**) an iterable object into individual elements. 
- Denoted by `...` 
- The spread syntax can be used with arrays, objects, and function arguments.
- The way to visualize it, everytime seen a spread operator, take out the enclosed symbols of the iteratable object and that is the output
- **Rule**: `...` before the iterable object

## Combining Arrays
- Combines arr1 and arr2 into a new array
```js
let arr1 = [1, -21, 3, 4];
let arr2 = [9, 3, -8, 10, 7];

const arr3 = [...arr1, ...arr2]; 
//  [1, -21, 3, 4, 9, 3, -8, 10, 7]

Math.max(...arr1, ...arr2)
// => 10
```

## Break Strings
```js
let string = "CMSCXYZ";
let charArray = [...string]
// => [C,M,S,C,X,Y,Z]
```

## Function Params
```js
let arr = [1,2,3]

callFun(...arr, "World") // callFun(1,2,3, "World")
```

## Objects
```js
const person = {
  firstName: 'John',
  lastName: 'Doe',
  age: 30,
  city: 'New York'
};

const employee = {
  ...person, // extracts person Obj
  position: 'Software Engineer',
  salary: 100000
};

console.log(employee);
// => 
//{
//  firstName: 'John',
//  lastName: 'Doe',
//  age: 30,
//  city: 'New York',
//  position: 'Software Engineer',
//  salary: 100000
//}
```


# 3️⃣ Chaining (`?`) Operator
- Placed after a property is accessed, which prevents access to the next level if the property does not exist
- If Chaining prevents the next call, ends the function call as if it had never been called

Let's defined two objects:
```js
const mary = {
    name: "Mary",
    address: {
        city: "College Park",
        state: "Maryland",
        budget: {
            local: 340,
            federal: 500,
        },
     },
};

const peter = { name: "Peter" };
```


**Problem**: reuse the same function to different Objects
```js
function printInfo(student) {
    document.writeln(`
        ${student.name}, ${student.address.city}, ${student.adress.state}`
    );
}

printInfo(peter); // TypeError undefined adress.city
printInfo(mary); // No Error, but Not printed because previous error
```


**Solution**: use chaining operator
```js
function printInfo(student) {
    document.writeln(`
        ${student?.name}, ${student.address?.city}, ${student.adress?.state}`
    );
}

printInfo(peter); // next
printInfo(mary);  // Mary, College Park, Maryland
```


# 4️⃣ `&&`, `||`, `??` Operators

## **logical (`&&`)** 
- If the first operand evaluates to FALSE, the first operand is returned; otherwise, the second operand is returned
	- Whatever makes it FALSE, the value's returned
- **Idea**: `&&` stops when there is one FALSE, therefore return operand when FALSE
```js
10 && 20         // 20  
true && 10       // 10  
false && 10      // false  
undefined && 10  // undefined  
null && 10       // null
10 && null && 20 // null
10 && 5 && 20    // 20
// issue
0 && true        // 0 is considered false, returns 0
```

## **Logical (`||`)** 
- If the first operand evaluates to TRUE, the first operand is returned; otherwise, the second operand is returned
	- Whatever makes it TRUE, the value's returned
- **Idea**: `||` stops when there is at least one TRUE, therefore return operand when TRUE
```js
// quantity = quantity || 20;
quantity ||= 20
//--------------------------//
10 || 20         // 10  
true || 10       // true  
false || false   // false
undefined || 10  // 10  
null || 10       // 10
// issue
0 || true          // 0 is considered FALSE, so return true
```


## **nullish coalescing operator (`??`)**
- Returns the value of the second operand if the left operator is null or undefined. 
- **Idea**: Pick left first, if left is NULL or UNDEFINED, then pick right operand.
```js
// quantity = quantity ?? 18;
quantity ??= 18;
//-----------------------//
20 ?? 18        // 20
null ?? 18      // 18
undefined ?? 18 // 18
// no issue
0 ?? 18         // 0 
```

