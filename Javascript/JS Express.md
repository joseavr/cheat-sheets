# JS Express

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-04-10

---
# 🎬 Intro to Express
Popular and lightweight web application framework for Node.js that simplifies the process of building robust, scalable and flexible web applications. Express simplifies the implementation of tasks that requires significant effort such **HTTP module**

- What Express provides:    
	- Extensions
	- Middleware  
	- Routing
	- Views

- Initialize project with Express
```js
/* Accessing express module */
const express = require("express"); 
/* Initialize express app */
const app = express(); 
```

# 😱 Things to Know
Before continuining we must know these terminologies. Here we go :)

## 1️⃣ HTTP Verbs/Methods
HTTP methods are useful to develop **REST** applications, consume APIs, deploy own server of resources, etc.

### **Request**
- `GET.request` - get or fetch data from server. Eg: loading standard html page, loading assets like json, css, images, etc.

- `POST.request` - posting data or adding smth in the server. 

- `PUT.request` - updating data already on the server

- `DELETE.request` - delete data from the server  

### **Response**
- `GET.POST.PUT.DELETE.response` - sends back smth from the server to the client. That smth can be: html page, route, message, etc.

*Note: Always use return when using `response` to avoid error when having double `response` in the code*


# 🧩 Extensions
The basic request and response objects have extra functionality. 
- `request.ip` - ip address
- `request.get` - to obtain HTTP headers
- `request.status` - to set status code
- `request.send`
- `response.redirect`
	- Redirects to a particular site
- `response.sendFile`
	- To send a file
- `response.json` - sending JSON response

# 🎭 Middleware
Middleware are basically functions in Express that validates *INPUTS* before sending an *OUTPUT* to a server.
- We can intercept the `request` from user before the `response` from server. **This is useful to authentication, logging, and error handling**.
- A middleware function can modify the **request** or **response** objects

**Example**:
- In a login page, If a user sends an invalid *password*, the middleware can intercept this *password* before sending the `request` to the Database. 
- If the *password* is not valid, then the middleware DOES NOT send the `response` back to the user.

## Code
We use the `app` variable with `.use()` to add new middlewares

How a middleware looks like? Here are some exmaples:
```js
// Importing Modules
const path = require("path")
const express = require("express")
const flash = require("connect-flash")
const csrf = require("csurf")
// Using these modules
const app = express()
const publicPath = path.resolve(__dirname, "staticFolderName") // Create path same for Linux, Mac, Windows

// Middleware to read static file
app.use(express.static(publicPath))

// Middleware for Flash messages
app.use(flash())

// Middleware to add CSRF protection to our app
app.use(csrf())

// Simple Middlewares that uses request and response to display messages
app.use((request, response, next) => {
  console.log("Received: " + request.url);
  message = "First middleware function\n";
  console.log(message);
  next(); /* go to next middleware function, needed if have a next middleware */
});

app.use((request, response) => {
  let secondMessage = "Second middleware function";
  console.log(secondMessage);
  message += secondMessage;
  response.end(message);
});

```


# 🚏 Routing
Routing allows us to associate an URL and an HTTP method. 
- Routes are defined using HTTP methods such as GET, POST, PUT, and DELETE and can be used to handle different types of requests. 
- Routes with **method GET** are oftenly to display HTML or retrieve data from server.
- Routes with **method POST** are oftenly when the HTML has a form and a submit button that changes the server.
- We no longer use `app.use()` (this is for middlewares), we use instead `app.get()`, `app.post()`, `app.put()`, etc.
- A website can have different routes
	- `/`
	- `/register`
	- `/login`
	- `/user`
	- `/user/settings`

**Example**: 
- We can have a route `/login` with method GET, which retrieve a HTML page (GET response) that has forms necessary to register an user.
- We can have another route `/login` with method POST. When user clicks on submit button, the data will be sent to the server, we can get the user inputs with **POST request**. Returns their user home page (POST response) if login sucessful, otherwise `/login` page (POST response) if no succesful.

## Code
```js
app.get("/login", (request, response) => {
  response.render("login.html") // renders a html when enters to this route
})

app.post("/login", (request, response) => {
  // POST request to get data sent by user then validate
  ..code..
  // POST response to send a html back to the user
  response.render("user.html")
})

app.put()

app.delete()
```

## 🆚 Params vs Query vs Body

- `req.params` - an object containing properties of the URL. For example, in the route `/users/:id`, the `id` parameter can be accessed with `req.params.id`. These parameters are defined in the route definition using `:` before the parameter name.
```js
// Route definition: GET /users/:id
// When user type: localhost:5000/users/123
app.get('/users/:id', (req, res) => {
  const extract_params = req.params; // -> { id: 123 }
  const extract_id = req.params.id; // -> 123
});
```
*Note: `req.params` is an object of key-value pairs and we use `.id` to its value*

- `req.query` - an object containing properties for each query string parameter in the URL. Query string parameters are appended to the end of a URL after a `?` character and separated by `&` characters. For example, in the URL `/search?q=term&page=2`, the `q` and `page` parameters can be accessed with `req.query.q` and `req.query.page`, respectively.
```js
// Route definition: GET /users/:id
// When user type: localhost:5000/users/search?q=term&page=2
app.get('/users', (req, res) => {
  const extract_query = req.query /// -> { q: term , page: 2 }
  const q = req.query.q; // -> term
  const page = req.query.page; // -> 2
});
```

- `req.body` - an object containing properties of the data submitted by an HTML form.
```js
// User subbmited a form: name = jose , password = 123
app.post('/users', (req, res) => {
  const extract_body = req.body; // -> { name: jose, password: 123 }
  const name = req.body.name // -> jose
  const password = req.body.password // -> 123
});
```


## Testing Server
We can test our routes to see if they work with `curl` in the shell command
```bash
curl -Method get http://localhost:8001
curl -Method post http://localhost:8001
curl -Method delete http://localhost:8001
```

However, there is something even more powerful, called [PostMan](https://www.postman.com/).
Among a lot things Postman offers, it allows you issue HTTP requests.

Another lightweigth app to issue only HTTP request is [Insomnia](https://insomnia.rest/)


# 🔭 Views/Template Engines
Express supports template engines such as Pug, EJS, and Handlebars, among others. Called Dynamic HTMLs.
- Useful for reusing repeating HTML layouts in different HTML files in our project and allows us to use JS code into HTML
- So useful!!

Suppose we have a route, we can send variables in the `render()` to pass to the `welcome.html`!!
```js
app.get("/", (request, response) => {
  const variables = {
    semester: "Summer",
    greeting: "Welcome to the course site"
  }
  response.render("welcome", variables); //Passing variables to welcome.html
});
```

The `semester` and `greeting` variables are passed to `welcome.html`
```html
// welcome.html
<body>
  <h1>Introduction (<%= semester %>)</h1>
  <p>The usual greeting is <%= greeting %> </p>
</body>
```

## Set Up Template Engines
- In order to use a template engine, we must set this up to our app
- We gonna use `app.set()`, which means "set up this to our app"

To specify the engine template, we gonna do two things:
- Set template engine extension: `.ejs`
- Set the folder where EJS files (aka views) are located
```js
const express = require('express')
const app = express()

app.set('view engine', '.ejs') // set extension ejs
app.set('views', './templates') // In templates folder are our ejs files
```

**Warning** ⚠️
If you are working on macOS or Windows, we recommend use `path.resolve` which will give you the full path no matter what OS you working on. This might fix some issues when working on macOS or Windows the same project.

The `path.resolve()` takes two arguments:
- `__dirname` - built-in node variable, full path of your project
- `<./folder>` - the folder where your HTMLs/Template Engine are located
- Returns the full path of your Template Engine folder that works for Windows/macOS/Linux
```js
const path = require('path') //necessary for resolve()

const FULLPATH = path.resolve(__dirname, './templates')
app.set('view engine', '.ejs') // set extension ejs
app.set('views', FULLPATH) // resolved path

```



# 📖 Read Input from Forms/Send Data with Template Engine
To let your app read inputs from Forms, you must activate it

```js
const express = require('express')
const app = express()
const bodyParser = require('body-parser')

// app.use(express.urlencoded({extended:true})) // my preference

// Active reading user input from Forms - Instructor notes
app.use(bodyParser.urlencoded({extended:false}));
```

Our app now can read inputs from user forms, but how can we catch those inputs?
- In a method post (meaning when an user press a submit button), the user inputs will be saved in the `body`, specifically in the `request.body`
- We can create an object to store these `request.body.semester` and `request.body.teacher`
- Or we can use destructuring on `request.body` to get these inputs (preference)
```js
app.post("/". (request,resposne) => {
  // Using destructuring - Preference
  // const {semester,teacher} = request.body
  
  // Using object - Instructor notes
  const variables = 
  {
	semester: request.body.semester,
	teacher: request.body.teacher
  },
  // Generate HTML and passing this variables
  response.render("courseInfo", variables);
})
```

But, you may ask, How do I actually know the user's inputs are called `semester` and `teacher` and are store in the `request.body`? The answer: the `name` attribute!!
- Note that when user fill the fields `Semeter:` and `Teacher:`, these values are store in body as `request.body.semester`  and `request.body.teacher` 
- `semester` and `teacher` because of the placeholder `name="semester"` and `name="teacher"` respectively.
- This is how we catch these values into our index.js - app.post()
```html 
<form action="http://localhost:7003/" method="post">
  <strong>Semester: </strong><input type="text" name="semester">
  <strong>Teacher: </strong><input type="text" name="teacher">
  <input type="submit" value="Submit Data">
</form>
```

Now that we have access to user inputs, we can send these variables to another HTML.
In brief, `semester` and `teacher` from the form will go thru `app.post()`, then `app.post()` will catch these variables and will send to another HTML using the template engine EJS.
- `<%= semester %>` means that we gonna replace **THIS** with an variable called `semester`
- `<%= teacher %>` means that we gonna replace **THIS** with an variable called `teacher`
```html
<!doctype html>
<html lang="en">
  <head>
  <title>Course Web Page</title>
  <meta charset="utf-8" />
</head>

<body>
  <h1>Course Information</h1>
  <p> 
	  Additional information for the 
	  <strong> <%= semester %> </strong> semester taught by 
	  <strong> <%= teacher %> </strong> is available on the CS Dept web site.
  </p>
</body>
</html>
```