# JS Flash Messages

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-04-30

---
# 🎬 Intro to Flash

Flash messages are used to display status messages to users after they perform an action on a website or application. 

They are often used to indicate whether an action was successful or not, and can provide useful feedback to the user.

# Set Up Flash Globably

In Node.js, you can set up flash messages using middleware such as `connect-flash` or `express-flash`. Here's an example using `connect-flash`:


1. First, install `connect-flash` by running the following command in your project directory:
```bash
npm install connect-flash`
```

2. Next, require `connect-flash` and initialize it in your app:    
```js
const flash = require('connect-flash');
const express = require('express');
const app = express();  app.use(flash());
```

3. Create an `app` object and set up session middleware with `express-session`:
```js
const app = express();

app.use(session({
  secret: 'your-secret-key',
  resave: false,
  saveUninitialized: false
}));
``` 

4. Initialize the `connect-flash` middleware to add flash messages to the response object:
```js
app.use(flash());
```

5. Create middleware to add flash messages to the response locals object for all routes:
```js
app.use((req, res, next) => {
  res.locals.success_messages = req.flash('success');
  res.locals.error_messages = req.flash('error');
  ...
  next();
});
```
*Note: Here, we're adding two properties to the `res.locals` object: `success_messages` and `error_messages`. We're using the `req.flash()` method to retrieve flash messages from the session for the `'success'` and `'error'` categories, and adding them to the response locals object.*


6. Use the `req.flash()` method to create flash messages. For example, to create a success message:    
```js
app.post('/login', (req, res) => {
  // Check if login is successful
  if (loginSuccessful) {
    req.flash('success', 'Login successful!');
    res.redirect('/dashboard');
  } else {
    req.flash('error', 'Invalid username or password');
    res.redirect('/login');
  }
});
```

7. Use the `success_messages` and `error_messages` properties in your views to display flash messages:
```js
<% if (success_messages && success_messages.length > 0) { %>
  <ul class="success-messages">
    <% success_messages.forEach(function(message) { %>
      <li><%= message %></li>
    <% }); %>
  </ul>
<% } %>

<% if (error_messages && error_messages.length > 0) { %>
  <ul class="error-messages">
    <% error_messages.forEach(function(message) { %>
      <li><%= message %></li>
    <% }); %>
  </ul>
<% } %>
```
*Note: Here, we're checking if the `success_messages` and `error_messages` properties exist and contain any messages before displaying them.*