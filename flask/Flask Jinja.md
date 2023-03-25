# 🌶️ Flask Jinja
Class: <a href=""> </a>

Subject: #

Date: 2023-03-24

Topics: #, #, # 

---

# 🎬 Intro to Jinja Engine
- Template engine used in Flask
- Allows to embed Python code within HTML templates.

# 1️⃣ Block Code `{% block ... %}`
- Defines a html block that can be overridden or extended by child html templates.
- Makes easy to reuse and organize html templates.

## Rule 
- `{% block <block_name> %}`
```html
<!-- in base.html -->
<head> ... </head>
<body>
	{% block header %}
	<h1>This content is overriden</h1>
	{% endblock %}
</body>
```

- In a child template, `{% extends <parent_html> %}` is required
- `{% block <block_name> %}`: block name must be the same as in the parent template to be overriden
```html
<!-- child template -->
{% extends "base.html" %} 
{% block header %}
	your code here
{% endblock %}
```

# 2️⃣ Comments `{# ... #}`  
- Add two (#) to add an comment

# 3️⃣ Expressions `{% ... %}` 
- Embed expressions such as
	- if-else
	- for
	- while
	- with open

# 4️⃣ Variables `{{ ... }}`
- Embed Python variables