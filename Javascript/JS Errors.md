# JS Errors

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 0101

🗓️Date: 2023-03-29

---

# Intro to Errors
There are many kind of Errors in Javascript.
- URIError
- TypeError 
- EvalError 
- Error while using eval()
- RangeError
- SyntaxError 
- ReferenceError
- and much more!

What if we want to catch an error inside a code block? Use Try-Catch

# Try - Catch
Here is an example of try-catch
```js
try {
  // This block may throw an error
  const result = someFunctionThatMightThrowAnError();
  console.log("Result:", result);
} catch (error) {
  // If an error occurs, this code will execute
  console.error("An error occurred:", error);
}
```

**Notes**:
- It's a good practice to use try-catch blocks when dealing with with external resources or user input. 
- This way, you can ensure that your application handles errors gracefully and doesn't crash or produce unexpected results.


# Throw Exception
What if we want to define our own errors:
- Use `function` so that we can create a class `DivideZeroError` for our custom Error
- Pass `message` and `value`
- Set the `prototype` of DivideZeroError to a new instance of Error() - this will ensure that DivideZeroError be a child class of Error class, (Inheritance).
```js
function DivideZeroError(message, value) {
  this.message = message;
  this.value = value;
}
// We need this so that all `DivideZeroError` be a child of `Error`
DivideZeroError.prototype = new Error();
```

Implementation:
```js
try {
  let a = 5, b = 0;
  
  if (b === 0) {
    // throw our own Error
    throw new DivideZeroError("Divide by zero error!", b);
  } else { 
    console.log(a / b) 
  }
    
} catch (error) {
  // If an error occurs, this code will execute
  alert(error.message + ", " + error.value);
}
```
- **Note**: `error` is an instance of the class `DivideZeroError`, which means we can access the `message` error and the `value` that caused the error.