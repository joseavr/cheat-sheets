# 💻 HTML Forms
Class: [[HTML]]
Subject: #
Date: 2023-02-13
Topics: #, #, # 

---

# 🎬 Intro 
- Interact between user and web
- Grab some data from a `form` and send it to a server
```html
<form action="" method="">

</form>
```

# 🏃 Action
- Indicates where the form contents will be sent when the form is submitted. It represents a script/program that will process the data.

#  💨 HTTP Methods
- Defines how the contents will be sent

## HTML GET
- HTTP GET is used to **retrieve data** from a server. 
- When a client sends an HTTP GET request to a server, it is asking the server to send back a resource (such as a web page) specified by a URL. 
- The data sent in an HTTP GET request is included in the URL as query parameters.
	- Parameters start after a question mark (?) and are separated by (&)
- Examples such as Google Search
- All form information appears in the URL
- Not good for security as information available in the URL
- There is a limit of data (parameters) as the URL has a size limit
- Look up operations, look data. 
- Doesn't modify the change of the server.
- `<form method="get">`, the data in the form is appended to the URL as query parameters, and the resulting URL is sent as an HTTP GET request to the server.

## HTTP POST
- HTTP POST is used to **send data** to a server.
- All kind of information is sent in the request body. 
	- Information such as plain text, JSON or XML.
- Secure than HTTP GET
- Better for security as information is not in the URL. Content is "hidden"
- You can modify the state of the server with POST
- `<form method="post"`, the data in the form is sent as an HTTP POST request to the server, with the data included in the request body.

## HTTP PUT

## HTTP DELETE

# Form Validation
- Stop Submit button to send the form to the server
- Instead check the form before send the data to the server
```js
/* IMPORTANT: Setting the function to call when submit is selected */
window.onsubmit = validateForm;

/* This function must return true or false
If true the data will be sent to the server.
If false the data will not be sent to the server */

function validateForm() {
	/* Retrieving the values */
	let name = document.getElementById("name").value;
	let account = document.getElementById("account").value;
	let payment = document.getElementById("payment").value;
	
	/* Validating numeric values */
	let invalidMessages = "";
	if (String(parseInt(account)) !== account) {
		invalidMessages += "Invalid account number provided.\n";
	}
	
	if (Number(payment) <= 0) {
		invalidMessages += "Invalid payment amount provided.";
	}
	
	if (invalidMessages !== "") {
		alert(invalidMessages);
		return false;
	} else {
		let valuesProvided = "Do you want to submit the following payment?\n";
		valuesProvided += "Name: " + name + "\n";
		valuesProvided += "Account: " + account + "\n";
		valuesProvided += "Payment: " + payment + "\n";
		/* We could write the following as return window.confirm(valuesProvided) */
		return window.confirm(valuesProvided);
	}
}
```