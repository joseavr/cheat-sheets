# JS Generator

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-05-03

---
# 🎬 Intro to Generator

- Like Ruby codeblocks

```js
function * getOddValuesGenerator() {
	let value = 1;
	
	while(true) {
		yield value;
		value
	}

}
```