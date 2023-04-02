# 🌶️ Flask User Management
Class: <a href=""> </a>

Subject: [[Flask]]

Date: 2023-03-23

Topics: #, #, # 

---

# 🎬 Intro 
- User Management is the ability to 
	- Provide user accounts
	- Secure registration/login/account recovery
	- Manage permissions between users
	- Encryp data & hash password
	- Back up data
	- Protect users' data and privacy form bad actors

# 🔐 Hashing Passwords

```bash
pip3 install flask-bcrypt
```

```python
from flask_bvcrypt import Bcrypt

app=Flask(__name__)
app.config['SECRET_KEY'] = '...'
bcrypt = Bcrypt(app)
```

## Password to a Hash
```python
hash = bcrypt.generate_password_hash('a_password') # returns byte string
=> b`...`

hash.decode() # returns a string
=> `...`
```

## Hash to Password
```python
bcrypt.check_password_hash(hash, 'a_password')
=> True
```

# 👤 User Sessions
- Ability to maintain user authentication state across multiple requests
- Flask Login allows to easily handle user authentication and authorization.

## Flask Login
- `flask_login` provides a global variable `current_user`
- We can check if `current_user` is:
	- `.is_authenticated`
	- `.is_active`
	- `.is_anonymous`
	- `.get_id()`
```python
flask_login import (
	LoginManager,
	current_user,
	login_user,
	logout_user,
	login_required
)
```

- To make the entire app flask_login compatible, we need to initiate the LoginManager class and specify where the login page is
- If an unauthenticated user tries to access a hidden part of our website, flask_login redirects them to the login page
```python
from flask_login import LoginManager

login_manager = LoginManager(app)
login_manager.login_view = 'login'
```

## Flask MongoEngine
- Helps enforce our Schema class
- Check [[Flask Models Schema]] to learn more about how `user_current` and `Model Schema` are connected
```python
from flask import Flask
from flask_mongoengine import MongoEngine

app = Flask(__name__)
app.config['MONGODB_HOST'] = ".../<db_name>"
app.config['SECRET_KEY'] = b'...'

db = MongoEngine(app)
```

## Restricted view
- Set `@login_required` to set the route only available for logged-in users
```python
from flask_login import login_required

@app.route('/some_restricted_route')
@login_required
def a_restricted_page():
	#some code
	return render_template()
```

### Render templates based on logged-in user
- `current_user` is automatically available for use in any templates! (HTML files)
```html
{% if current_user.is_authenticated %}
  <h1> Hello {{ current_user.username }}! </h1>
  <h2> This is your email: {{ current_user.email }} </h2>
{% endif %}
```

## Login
```python
from flask_login import login_user, current_user
from flask_app.forms import LoginForm
from flask_app.models import User

@app.route("/login", methods=['GET', 'POST'])
def login():
	# If the current user is authenticated, then 
	# they don’t need to see the login page, so redirect them
    if current_user.is_authenticated:
        return redirect(url_for('index'))

    form = LoginForm()

	# If the login form is validated…
    if form.validate_on_submit():
	    # Attempt to find the appropriate user
        user = User.objects(username=form.username.data).first()
		# If valid (user exists and input password’s hash matches)
        if (user is not None and bcrypt.check_password_hash(user.password, form.password.data)):
            login_user(user) # login user
            return redirect(url_for('account'))
    
    return render_template('login.html', title='Login', form=form)**
```

## Registration
```python
@app.route("/register", methods=['GET', 'POST'])
def register():
    if current_user.is_authenticated:
        return redirect(url_for('index'))
    form = RegistrationForm()
    if form.validate_on_submit():
        hashed = bcrypt.generate_password_hash(form.password.data).decode('utf-8')
        user = User(username=form.username.data, 
                    email=form.email.data, password=hashed)
        user.save()
        return redirect(url_for('login'))

    return render_template('register.html', title='Register', form=form)**
```

## Logout
-   Flask_login provides a logout_user function
```python
from flask_login import logout_user
@app.route("/logout")

def logout():
    logout_user() # logout user
    return redirect(url_for('index'))
```