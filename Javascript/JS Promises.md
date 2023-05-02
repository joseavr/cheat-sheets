# JS Promises

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 0101

🗓️Date: 2023-03-06

---

# 🎬 Intro to Promises
- We first need to understand what is an **Object**
- Collection of properties
- `Property`: like a dictionary
	- A property can be seen as a variable associated with a value
		> obj.propertyName = "Mary"
	- A property can be accessed with `key`-`value`
		> obj["propertyName"] = "Mary"

# 🆕 Create Objects
- Using Object constructor
	- Creates an object for the given value
		- let x = new Object(true);
	- If parameter passed is `null` or `undefined`, an empty object will be created
- Using Object initalizer
	- let x = {}
	- y = { radius: 20}
- Using `Object.create()`
	- Objects.html 
	- AddingProperties.html

# 📦  Promises
- An object that represents the eventual completion (or failure) of an `asynchronous operation`
- A promise can return: **JSON**, **text**, **statusCode**, **headers**, etc

- We attach callbacks to the promise object
	- Allows `promise chaining`
		- Execution of two or more asynchronous operations 
```js
const promise = fetch(url);

promise   // Asynchronous task
	.then(response => response.json())
	.then(json => console.log(json))
```

# 🆚 Async vs Await
- `Asynchronous`: does not block the execution. Means that the HTML will load even if the asynchronous task (e.g fetching from web, api, etc) takes long time.
	- Fetch is asynchronous by default.
	- Analogy: An asynchronous task can be executed simultaneously while other code is executing
- `await`: synchronize the task. The HTML waits until the task is completed.
	- Analogy: Code is executed line by line


# 📤 Fetch API
- Provides ability for fetching resources (from web)
- Takes one argument: the path of the source
	- Returns a `promise`
- By default, we are generating a GET request
	- A second option parameter allows to issue POST, PUT, DELETE request
- URL has to be absolute URL
- Response object (return value) has methods/information such as:
	- `json()` - parses the body of the response into JSON obj and returns error if the parsing fails
	- `text()` - returns the body of the response as text
	- `status` and `statusText` - information about HTTP status code
	- `ok` - true if the status is a 2xx status code
	- `Headers` - object containing headers, a specific header can be accessed using the `get()` function.

**Rule**:
```js
fetch(url [, options]);
```
**Options**:
```js
{ method: "PUT", // GET, POST, PUT/PATCH, DELETE 
  body: JSON.parse(data), // stored in req.body
  headers: { "Content-Type": "application/json" }
```
- `url`: The URL of the resource you're requesting.
- `{ method: "PUT" }`: HTTP method using to make the request. In this case, PUT request.
- `{ body: JSON.parse(data) }`: Data sending with the request. Sent as the request body.
- `{ headers: { "Content-Type": "application/json" } }`: Additional information about the request, including metadata about the data being sent. In this case, the header specifies that data sent is in JSON format.

As for examples of other content types that could be specified in the `Content-Type` header besides `application/json`, here are a few:
-   `text/plain`: Specifies that the content is plain text.
-   `multipart/form-data`: Specifies that the content is a set of key-value pairs that represents a form to be submitted.
-   `application/x-www-form-urlencoded`: Similar to `multipart/form-data`, but encodes the form data as a URL-encoded string instead.

Besides `Content-Type`, there are also:
- `Accept`: Specifies the media types that are acceptable for the response. For example, `Accept: text/html` indicates that the client can accept HTML content in response.
- `Authorization`: Specifies the authentication credentials required for the request. For example, `Authorization: Bearer <token>` might be used to send an access token for authentication.
- `Content-Type`: Specifies the format of the data being sent in the request body. We've already seen an example of this header in the original code snippet you provided.
- `User-Agent`: Specifies information about the client making the request. For example, `User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3` provides information about the user's web browser and operating system.


## Calling Fetch Asynchronous
```js
// json()
let url = "https://jsonplaceholder.typicode.com/posts/1" 
fetch(url) // get data
    .then(res => res.json())

// text()
	.then(res => res.text())

// status
	.then(res => res.status)
// ok
	.then(res => res.ok)
// header
	.then(res => res.headers.get('content-type'))
```

## Calling Fetch with Await (Synchronous)
```js
async function fetching(){
  const json = await fetch(url).then(res => res.json())
}
```

Another way: 
```js
// It's always good enclose this by try-catch
// since we are http request a server and we dont 
const response = await fetch(url); 
const data = await response.json();
```
*Note: It's always good practice to enclose by try-catch since we are http request a server and we don't if request fails or not*


# 🧇 Destructuring JSON
```js
fetch(url)
	.then(response => response.json())
	.then(json => processObject(json));


function processObject({userId, id, title}) { // notice destructuring
	console.log("Data Retrieved\n");
	console.log(`user Id: ${userId}`);
	console.log(`id: ${id}`);
	console.log(`title: ${title}`);
```

- [More JSON functions](<./JS JSON>)

# 🤷🏻‍♂️ What is API
- Application Programming Interface (API)
- APIs to draaw and manipulate graphs: Canvas and WebGL
- APIS audio and media: HTMLMediaElement, Web Audio API, and WebRTC
- API devices: geolocation, system vibration, etc
- APIS de almacenamiento en el lado del cliente: Web Storage API (sessionStorage, localStorage), IndexedDB API.
- Google maps
- Facebook, Twitter, Instagram, Discord, Youtube, etc
- jsonplaceholder


# 🛏️ API REST
- Representational State Transfer (REST)
- Build own API for communication between FrontEnd and BackEnd
- Rest is a technique to build APIs using protocole HTTP thru URIs, smart enough to satisfy the needs of a client
- API Rest is a just a way to send resources so that it can be used
- Uses HTPP: GET, POST, PUT, DELETE


# 🛌 RESTFul
- REST is the concept
- RESTFul is the implementation
- By creating a RESTFul, we creating an API
- API is a set of functions or procedure so that it can be used by another software


# ➡️ Response Status
## Informational (100-199): 
Indicates the server has received the request and is continuing to process it.

## Success (200-299): 
Indicates the server successfully processed the request and returned the expected response.

## Redirection (300-399): 
Indicate the requested resource is not available at the expected location and the client should try a different location.

## Client error (400-499): 
This category includes codes that indicate an error on the client's part, such as a malformed request.

## Server error (500-599): 
This category includes codes that indicate an error on the server's part, such as a server-side error or timeout.

