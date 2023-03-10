# JS Events
Class: [[JS]]
Subject: #
Date: 2023-03-06
Topics: #, #, # 

---

# ➡ Arrow Functions
- As known as Lambda Expressions (`=>`)
## Rule
```js
parameter => code
```
- Parenthesis is required if
	- No parameters
	- Two or more
```js
/* No parameters */
let initialValue = () => 1000;
document.writeln("initialValue(): " + initialValue() + "<br>");
```
- Parenthesis is not required if
	- One parameter
```js
/* One parameter and expression as returned value */
let prod2 = x => x * 2;
document.writeln("prod2(10): " + prod2(10) + "<br>");
```
- Curly bracket if function takes more than 2 lines
```js
/* We need curly brackets */
let formatted = x => {
	x++;
	return `Value: ${x}`; /* return is needed */
};
```

# 🎟️ Events
- Notification of something has occurred
- Example of events:
	- Browser finishes loading document
	- When the user clicks on a button
	- When the user moves the mouse
	- Others
- Event handler (a.k.a `event listener`)
	- JS function or code fragment that is executed when a particular event occurs
- Event handler registration
	- Associating an event handler with a particular event

# 🆚 Difference of Event-driven Programming
## Normal Programming
- Start at main()
- Continues until the end of the program or exit()

## Event-driven Programming
- Start at main()
- Register event handlers
- Await events & perform associated computation

## GUIS (Graphical User Interface)
- Example of event-driven programming softwares

# 📖 Event Handler Attributes for HTML
## Mouse Related
- `onclick` - moyse button is pressed and released
- `ondblclick` - mouse button is double-click over the element
- `onmousedown` - the mouse is pressed down while the cursor is over the element
- `onmouseup` - the mouse is released while the cursor is over the element
- `onmouseenter` - mouse moves onto the element
- `onmouseover` - mouse pointer enters into an element and its child elements
- `onmouseout` - mouse moves off an element
- `onmousemove` - mouse pointer is moved over an element

# ↪ Accessing Data From Text Fields

## Selecting an Element
- `document`: the DOM or tree representation of the HTML
- `querySelector` - selects ID like in css
```js
document.getElementById("elementId")
document.querySelector("#elementId")
```

## ↩ Retrieving Text from Element
- Retrieving text field using `.value`
```js
let login = document.getElementId("loginId").value;
=> login = "Sign In"
```

# 🔗 Associating Function with Event
- **Defining which function to call when an element (button) is clicked on**
```js
document.getElementById("processButtonId").onclick= callback;
```

- **Another way to associate a function is to use addEventListener**
	- Allows several events to be added
```js
document.querySelector("#displayTimeButton").addEventListener("click", () => alert(new Date()));
```

- **Another way is to set the onclick property in the element**
```html
<input type="button" value="Display SChool Name" onclick="displaySchoolName()" />
```
TODO EXAMples

# 📋 Form Data Access
- Access/Modify attributes using `getAttribute()` and `setAttribute()`
```js
let imageElement = document.getElementById("myImage");
let imageName = imageElement.getAttribute("src");
imageElement.setAttribute("src", “imageFile.jpg”);
```

- Access/Modify the attribute directly
```js
document.querySelector("#myImage").src = "testudo1.jpg"
```

- `getAttribute` vs `querySelector().src`
```js
imageElement.getAttribute("src"); // value of src
// images/Testudo1.jpg

document.querySelector("#myImage").src // full path
// http://127.0.0.1:5500/EventsICode/images/Testudo1.jpg
```

# 🆚  setTimeout vs clearInterval vs setInterval
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

# 📑 Modify Page with innerHTML
- `document.querySelector().innerHTML` - add/replace HTML code inside an element by ID (e.g div)
```js
document.querySelector("#mydiv").innerHTML = table // replace a new content to the element

document.querySelector("#mydiv").innerHTML += table // add new content to the element
```

- `document.writeln()` - write a string of text or HTML code to the document, followed by a line break.
	- It is typically used to add new content to the end of a document or a specific element
```js
// Write a string to the end of document
document.writeln("Hello, world!");

// Write HTML code at the end to a specific element
document.getElementById("myElement").writeln("<p>Hello, world!</p>");

```

# 📥 Loading JS File into HTML

## Attributes for Script Tag
- `defer` 
	- Indicates that the browser should not execute the script immediately when it is encountered in the HTML document. 
	- Instead, script will be downloaded in parallel with parsing the page and executed after the page has been parsed
	- No need to place `<script src=""` at the end of HTML file

- `async` 
	- The browser will download these scripts asynchronously while parsing the HTML document
	- The browser will execute them as soon as they are ready, even if they are not downloaded in the order they appear in the HTML document.
	- **Note**: 
		- "async" attribute is recommended for scripts that do not rely on other scripts or resources on the page, as the order of execution may be unpredictable. 
		- If scripts need to be executed in a specific order, the "defer" attribute may be a better choice.
```js
<!DOCTYPE html>
<html>
<head>
  <title>Async Script Example</title>
  <script src="script1.js" async></script>
  <script src="script2.js" async></script>
</head>
<body>
  <!-- Page content goes here -->
</body>
</html>
```

- `defer` or `async` missing
	- Script is downloaded and executed immediately
	- Blocks the page parsing until the script finishes downloading