# JS Event Propagation

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-05-03

---
# 🎬 Intro to Event Propagation

- When we have nested elements tags. We can control them with Event Propagation

## Example
- Suppose we have the following HTML
```html
```html
<div id="OuterElement">
	This text is part of the outer element.<br><br><br>
	<div id="InnerElement">
		&nbsp;&nbsp;This text is part of the inner element.
		<div id="WayInnerElement">
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This text is part of the way inner element :)<br><br><br>
		</div>
	</div>
</div>
```

- In this example, we click on the most inner element, then the second outer element's event is called, then third element's event is called with the event listener. 
	- If we click on the second inner element, the event is called, then the parent element event is called 
```js
document.getElementById("OuterElement")
	.addEventListener("click", () => alert("OuterElement"));

document.getElementById("InnerElement")
	.addEventListener("click", () => alert("InnerElement"));

document.getElementById("WayInnerElement")
	.addEventListener("click", () => alert("WayInnerElement"));
```
*Usefulness: we can define one `event listener` that can take care of all outer elements*

# Controlling the Propagation
- We control the propagation by setting a second argument in the `event listener` to
	- True: the event will start from most outer element to inner most (**Capturing**)
	- False: (or missing) the event will start from most inner to outer, ( **bubbling**), Otherwise capturing
- We can make the events work so that it always start at the top to the bottom no matter if the event is activated the inner elements
- Applications: A calculator
	- We dont have to set a listener to each button
	- We can define a parent listener that will process each buttons when clicked

```js
document.getElementById("OuterElement")
	.addEventListener("click", () => alert("OuterElement"), true);

document.getElementById("InnerElement")
	.addEventListener("click", () => alert("InnerElement"), true);

document.getElementById("WayInnerElement")
	.addEventListener("click", () => alert("WayInnerElement"), true);
```


# Accessing Element Event Occurrence

## Working with `this`
- The `this` is always linked to the object associated with the listener, no matter what
- If we create a object.eventListener, the `this` will refer to `object` no matter what
```js
/* Observe what "this" refers to */
innerElement
	.addEventListener("click", () => alert("InnerElement: " + this)
	// Here `this` refers to innerElement
	);
	

wayInnerElement
	.addEventListener("click", function (event) {
	alert("WayInnerElement" + this);
	// Here `this` refers to wayInnerElement
  });
```


# Stop Propagation  (Bubbling)
- We can stop propagation with `e.stopPropagation()` built-in function
```js
document
	.getElementById("OuterElement")
	.addEventListener("click", () => alert("OuterElement"));

document
	.getElementById("InnerElement")
	.addEventListener("click", (e) => {
  alert("InnerElement");
  e.stopPropagation(); // HERE WE STOP PROPAGATION
});

document
	.getElementById("WayInnerElement")
	.addEventListener("click", () => alert("WayInnerElement"));
```

# Video Camera
- Uses Browser api to stream using your device's camera
- Use `navigator.mediaDevices.getUserMedia`
```js
const video = document.querySelector(".camera"); // This is a div class="camera"

navigator.mediaDevices
	.getUserMedia({ video: true })
	.then(mediaStream => {
	  video.srcObject = mediaStream;
	  video.load();
	  video.play();
	})
	.catch(err => {
	console.log(err);
});
```