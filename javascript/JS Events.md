# JS Events
Class: [[JS]]
Subject: #
Date: 2023-03-06
Topics: #, #, # 

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


# ➡ Arrow Functions
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
- `ondblclick` - mouse button is double-click over the element
- `onmousedown` - the mouse is pressed down while the cursor is over the element
- `onmouseup` - the mouse is released while the cursor is over the element
- `onmouseenter` - mouse moves onto the element
- `onmouseover` - mouse pointer enters into an element and its child elements
- `onmouseout` - mouse moves off an element
- `onmousemove` - mouse pointer is moved over an element


# 🔗 Associating Function with Event
- **Defining which function to call when an element (button) is clicked on**
```js
document.getElementById("processButtonId").onclick = callback;
```

- **Another way to associate a function is to use addEventListener**
	- Allows several events to be added
```js
document.querySelector("#displayTimeButton").addEventListener("click", () => alert(new Date()));
```

- **Another way is to set the onclick property in the element**
```html
<input type="button" value="Display School Name" onclick="displaySchoolName()" />
```
TODO EXAMples


