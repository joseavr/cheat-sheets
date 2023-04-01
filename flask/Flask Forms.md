# 🌶️ Flask Forms
Class: [[Flask]]
Subject: #
Date: 2023-03-04
Topics: #, #, # 

---

# 🎬 Intro to Forms in Flask 

- Allow users to enter data on our website and process input with POST
- **Problem**: bad websites can send data to specific routes in our website
- These are called Cross-Site Request Forgery (CSRF) attacks

# 🔐 CSRF
## Cookies
- It is a packet of data your browser holds
- it sends to the server with a `request` and the server handles this with an appropiate `response`
- Cookies allows customizing `sessions` in our website
- The CSRF token should satisfy three requirements
	- Unique per session
	- Large, randomized value
	- Generateed by a cryptopgraphically secure pseudo-random number generator
- App must check token values match up
- We use the package `Flask-WTF`

## CSRF More Secure
- Limit cookie transport to HTTPS only
- Protect cookies from being read with JS
- Don't send cookies with CSRF-prone requests from external sites
```python
app.config.update(
	SESSION_COOKIE_SECURE=True,
	SESSION_COOKIE_HTTPONLY=True,
	SESSION_COOKIE_SAMESITE-'Lax',
)
```

# 👥 Sessions
- Sessions keep track of users'info between requests
- To use sessions, set `SECRET_KEY` for our app
- Generate a 16-byte random `key` 
```python
os.urandom(16)

# in terminal
python3 -c "import os; print(os.urandom(16))"

# set SECRET_KEY
app.configp['SECRET_KEY'] = b'.....'
```
- More about Session in [[Flask User Management]]

# 🗞️ Form Handling
- Form handling is easy with Flask-WTF package
```python
pip3 isntall Flask-WTF
```

## Form Fields
It takes two parameters: `ClassField( label_name:str` , `validator:lst )`
- `StringField()`
- `IntegerField()`
- `SubmitField()`
- …

## Form Validators
A `validator:lst` usually has:
- `InputRequired()`
- `Length(min:int , max:int)`
- `NumberRange(min:int , max:int , msg:str)`
- List of validators
	- https://wtforms.readthedocs.io

### Create own Validator
- Create custom validator with `validate_<name_field>()`
- **Example**: write a custom validator function for a field called "username" to check whether its length is greater than or equal to 1. If not, throw error
```python
from flask_wtf import FlaskForm
from wtforms import StringField, PasswordField, SubmitField
from wtforms.validators import InputRequired

class LoginForm(FlaskForm):
	username = StringField('Username', validators=[InputRequired()])
	password = PasswordField('Password', validators=[InputRequired()])
	submit = SubmitField('Login')
	
	def validate_username(self, username):
		strlen = len(username.data)
		if strlen < 1:
			raise ValidationError('Too Short!!!!')
	
```

## Example WelcomeForm
```python
class WelcomeForm(FlaskForm):
	name = StringFIeld('Name', validators=[InputRequired(), Length(min=4, max=30)])

	location = StringField('Location', validators=[InputRequired(), Length(min=3, max=50)])

	age = IntegerField('Age', validators=[InputRequired(), NUmberRange(min=1, max=140, message='Must be between 1 and 140')])

	submit = SubmitField('Submit')
```

# 🔄 Form - Method POST
- Assume we have a `WelcomeForm()` that post some data in a DB:
	- process data from form (HTML)
	- Validates when submitted
		- If valid, redirects to a route
		- If not valid, redirects to another route
- To validate our form in the HTML, pass `form` object into `render_template()`
```python
# routes.py
from flask import render_template, redirect, request
from forms import * # allows import all functions from forms.

@app.route('/', methods=['GET', 'POST'])
def index():
	form = WelcomeForm()  # form variable
	if request.method == 'POST' and form.validate_on_submit():
		# do stuff on the DB
		return redirect('/')
	# Renders this template when URL is '/'
	return render_template('index.html', title='Front page', form=form)
```

## Validate form in HTML
- How do we render `form` variable? We use it in the HTML
- The `form` variable provides CSRF token
- We can add attributes to the `form` fields 
```html
{% extends "base.html"}
{% block content %}
	<h1> Welcome to the website! </h1>
	<form action="/" method="post">
		<!-- Must csr_token -->
		{{ form.csrf_token }}
		<!-- a label for textfield -->
		{{ form.name.label(class="label", ...) }} 
		<!-- textfield -->
		{{ form.location.label(placeholder="Enter location") }}
		<!-- submit button -->
		{{ form.submit(class="submit") }}
	</form>
{% endblock %}
```
