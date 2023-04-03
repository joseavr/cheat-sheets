# JS Events

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 0101

🗓️Date: 2023-03-06

---

# 🎬 Intro to Events
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

## 🆚 Difference of Event-driven Programming
### Normal Programming
- Start at main()
- Continues until the end of the program or exit()

### Event-driven Programming
- Start at main()
- Register event handlers
- Await events & perform associated computation

### GUIS (Graphical User Interface)
- Example of event-driven programming softwares


# ➡ Arrow Functions (LAMBDA)
- As known as Lambda Expressions (`=>`)
- Rule:
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



# 📖 Event Handler Attributes for HTML
## Mouse Related
- `onclick` - mouse button is pressed and released
	- `.addEventListener("clikc", fun)`
- `ondblclick` - mouse button is double-click over the element
	- `.addEventLister("dblclick", fun)`
- `onchange` - Losing focus when pressed Enter or TAB
	- `.addEventLister("change", fun)`
- `onmousedown` - the mouse is pressed down while the cursor is over the element
	- `.addEventLister("mousedown", fun)`
- `onmouseup` - the mouse is released while the cursor is over the element
	- `.addEventLister("mouseup", fun)`
- `onmouseenter` - mouse moves onto the element
	- `.addEventLister("mouseenter", fun)`
- `onmouseover` - mouse pointer enters into an element and its child elements
	- `.addEventLister("mouseover", fun)`
- `onmouseout` - mouse moves off an element
	- `.addEventLister("mouseout", fun)`
- `onmousemove` - mouse pointer is moved over an element
	- `.addEventLister("mousemove", fun)`


# 🔗 Associating Function with Events
- **Call function when an element (button) is clicked on**
	- Only one function associated
```js
document.getElementById("processButtonId").onclick = callback;
```

- **Another way to associate a function is to use addEventListener (preferable)**
	- Allows several functions to be added
```javascript
document.querySelector("#displayTimeButton").addEventListener("click", () => alert(new Date()) );

document.querySelector("#displayTimeButton").addEventListener("click", () => function() );
```

- **Another way is to set the onclick property in the element**
```html
<input type="button" value="Display School Name" onclick="displaySchoolName()" />
```
