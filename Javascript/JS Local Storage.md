# JS Local Storage

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-04-12

---
# 🎬 Intro to Local Storage
- Allows to store data locally, with no expiration date.
- All of this are supported on the browser.
- Can only store strings. To store objects, you could use JSON.stringify()
- Not available on server-side
- Stored locally in the browser and is not tied to any specific session.
- Data will persist even if the user closes their browser and comes back to your website later.

- Set data
```js
localStorage.setItem("name", "Mary");
```

- Retrieve data
```js
localStorage.getItem(“name");
```

- Clean Local Storage 
```js
window.localStorage.clear()
```
*Note: Inspect in chrome -> console*

**Example**:
In mobile app games, when lose connection, the local storage restore your game


# 🪧 HTML5 Canvas
- For graphics, games
- Rectangular area of the page
- Can store canvas drawing as a image
- Example: [Excalidraw.com](https://excalidraw.com/)


# 🖼️ HTML5 SVG
- SVG - Scalable Vector Graphics
- Never lose resolution when you scale it, different as .png, jpge files
- You can embed it on HTML
```js
<svg width="100" height="100">  
  <circle cx="50" cy="50" r="40" stroke="green" stroke-width="4" fill="yellow" />  
</svg>
```

# 🌎 Geolocation API
- Example: Geolocation.html 
- In Chrome you will see at the top “Location blocked” to the left of the URL
- You can try the following link on your phone https://www.cs.umd.edu/~nelson/geoLocationExamples/ 
- Reference: – http://www.w3schools.com/html/html5_geolocation.asp

# 🫃🏻 Regular Expression
- Can create password strength, weak, etc
- Example: RegularExpressions.html

# 📁 FileReader API
- Another option using fetch() but
- We will use **input type="file"** to create a button to choose a file.
```html
<input type="file">
```

- Function to read an .txt
```js
let reader = new FileReader()
reader.onload = () => { 
  document.getElementByOd("displayArea").innerHTML = reader.result};

read.readAsText(filename);
```

- We can also read an image.
- Read JSONs too.

# 🔉 Sound 
- We can handle .mp3 files (sounds)
