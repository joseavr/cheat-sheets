# JS Ajax

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 0101

🗓️Date: 2023-03-29

---

# 🎬 Intro to Ajax
- AJAX, stands for Asynchronous Javascript And XML
- Before `fetch()`, there was AJAX that allows to issue HTTP request to a server (old technology)
- **Can generate HTTP request both GET and POST**

> How can we issue an HTTP request? (Possible Question Exam)
> > - With a form with method get/post
> > - fetch with get/post
> > - Axios get/post
> > - AJAX get/post

- When doing a HTTP request, oftently the page reloads/redirect to another page.
- Can the page be updated without being reloaded? Yes, with AJAX
- AJAX is async,
	- The requests are not synchronized with user actions (e.g., clicking on links, buttons, etc.). 
	- User can continue interacting with the browser while the request is being processed
