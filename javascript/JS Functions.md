#  JS Functions
Class: [[]]
Subject: #
Date: 2023-03-05
Topics: #, #, # 

---

# ✅ Useful Functions

## 1️⃣ Random RGB Color
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


## 2️⃣ setTimeout vs clearInterval vs setInterval
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
