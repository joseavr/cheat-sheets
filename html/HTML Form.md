# Forms
Class: [[]]
Subject: #
Date: 2023-02-13
Topics: #, #, # 

---

# Intro 
- Interact between user and web
- Grab some data from a `form` and send it to a server
```html
<form action="" method="">

</form>
```

# Action
- Indicates where the form contents will be sent when the form is submitted. It represents a script/program that will process the data.

# Method
- Defines how the contents will be sent

## HTML GET
- Contents are included in the URL. 
	- Parameters start after a question mark (?) and are separated by (&)

- All form information appears in the URL
- Not good for security as information available in the URL
- There is a limit of data (parameters) as the URL has a size limit
- Look up operations, look data. 
- Doesn't modify the change of the server.

## HTTP POST
- All form information sent as a message
- Secure than HTTP GET
- Better for security as information is not in the URL. Content is "hidden"
- You can modify the state of the server with POST

