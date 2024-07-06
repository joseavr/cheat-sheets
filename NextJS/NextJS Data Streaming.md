# Streaming Data

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-12-02

---

# Data Streaming for openAi

## Server

## Client 

```js
const [result, setResult] = useState('')

const res = await fetch(url, {
	method: 'POST',
	body: JSON.stringify(data)
	headers: {
		'Content-Type': 'application/json'
	}
})

// read data streaming
const reader = res.body.getReader() // <- read bytes
const decoder = new TextDecoder() // <- convert bytes to text

while (true) {
	const { done, value } = await reader.read() // read piece of bytes
	const chunk = decoder.decode(value)  // convert to piece of text
	setResult(chunk) // save in a state
	if(done) break // break inf-loop when processed all data
}
```

Advance version:
```ts
// Function Generator:
async function* streamReader(res: Response) {
	const reader = res.body?.getReader() // <- read bytes
	const decoder = new TextDecoder() // <- convert bytes to text
	if(reader == null) return
	
	while (true) {
		const { done, value } = await reader.read() // read piece of bytes
		const chunk = decoder.decode(value)  // convert to piece of text
		yield chunk
		if(done) break // break inf-loop when processed all data
	}
}

const res = await fetch(url, {
	method: 'POST',
	body: JSON.stringify(data)
	headers: {
		'Content-Type': 'application/json'
	}
})

for await (const chunk of streamReader(res)) {
	setResult((prev) => prev + chunk)
}
```

