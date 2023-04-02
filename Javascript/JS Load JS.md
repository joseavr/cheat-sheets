# JS Load JavaScript 

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 0101

🗓️Date: 2023-03-25


---

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