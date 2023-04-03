# HS How to Do

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-04-02

---

# 🤷🏻‍♂️ How to

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
