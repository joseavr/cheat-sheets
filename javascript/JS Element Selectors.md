# JS Element Selectors
Class: <a href=""> </a>

Subject: [[JS]]

Date: 2023-03-25

Topics: #, #, # 

---

# ↪ Accessing Data From Text Fields
## ☝ Selecting an Element
- `document`: the DOM or tree representation of the HTML
- `querySelector` - selects ID like in css
```js
document.getElementByClassName("elementClass")  // returns NodeList
document.getElementById("elementId")    // returns NodeList
document.getElementsByTagName('div')    // Returns NodeList
document.getElementsByName('interests') // <input name="interests">
// returns NodeList

document.querySelector("#elementId")    // returns the first instance
document.querySelector('.elementClass') // returns the first instance
```

## ↩ Retrieving Text from Element
- Retrieving text field using `.value`
```js
let login = document.getElementId("loginId").value;
=> login = "Sign In"
```


# ⬆️ Modify Element Attribute
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

# ⬆️ Modify Class Attribute
- Get `classList` and replace an element class with `replace()`
```html
<p id="my-paragraph" class="red">Hello, world!</p>
```
```javascript
element.classList.replace("red", "blue");
```

- `remove()` and `add()`
```javascript
element.classList.remove("red"); 
element.classList.add("blue");
```

- `toggle(<name>)`: 
	- If the element has the `<name>` class, it removes it (returns False)
	- if it doesn't have it, it adds it. (returns True)
```html
<p id="my-paragraph" class="red">Hello, world!</p>
```
```javascript
element.classList.toggle("blue");
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

