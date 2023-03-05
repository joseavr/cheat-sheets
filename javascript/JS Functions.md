#  JS Functions
Class: [[]]
Subject: #
Date: 2023-03-05
Topics: #, #, # 

---

# ✅ Useful Functions

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
