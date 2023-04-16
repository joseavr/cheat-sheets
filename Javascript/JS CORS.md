# JS Cross-Origin Resource Sharing

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-04-03

---
# 🎬 Intro to CORS

By default Web Browser denies access of web applications to another web apps from accesing its resources.

Imagine you have your website that provides info/data of all movies you can imagine. Since your web app denies access to another domains by default, with CORS you can allow access other websites to fetch your data/resources/API.  

It is just a security feature implemented in web browsers to allow other web pages fetch your website.

To enable CORS in JavaScript, you need to set the appropriate HTTP headers on the server that's serving the resources. For example, you can set the "Access-Control-Allow-Origin" header to specify which domains are allowed to access the resources.