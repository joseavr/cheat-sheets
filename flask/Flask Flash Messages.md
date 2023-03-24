# 🌶️ Flask Flash Messages
Class: <a href=""> </a>

Subject: #

Date: 2023-03-23

Topics: #, #, # 

---

# 🎬 Intro to Flash Messages
- Way to display feedback to the user after a particular action is performed, such as a successful login or an error during a form submission. 
- Flash messages are displayed on the next request
	- A redirection after a form submission.
- Uses cookies! - Must set secret key to ensure cookies are encrypted
```python
from flask import flash
```
# ⚡️Flash Messages with Categories
- Category can be any string
- Rule: `flash('message', 'category')`
- In Jinja, `get_flashed_messages()` needs to pass `with_categories=true` to destructuring `categories` in a for loop
```jinja
{% with messages = get_flashed_messages(with_categories=true) %}
```
## Example 
```python
from flask import  flash, Flask, render_template, request, redirect, url_for

@app.route('/', methods=['GET', 'POST'])
def index():
	# Another way using `request` instead of forms
    if request.method == 'POST':
        # Process the form submission
        name = request.form['name']
        email = request.form['email']
        if name and email:
            # Save the user's details to a database
            flash('Thanks for submitting the form!') # Flash Message
            return redirect(url_for('index')) 
        else:
	        # Flash Message with category
            flash('Please fill in both fields.', 'danger') 
    return render_template('index.html')
```

## Flash + Jinja + Bootstrap
- To display styled Alerts Messages with Bootstrap
- Reference: https://getbootstrap.com/docs/4.0/components/alerts/
```python
{% with messages = get_flashed_messages(with_categories=true) %}
  {% if messages %}
    {% for category, message in messages %}
      <div class="alert alert-{{ category }}">
        {{ message }}
      </div>
    {% endfor %}
  {% endif %}
{% endwith %}
```