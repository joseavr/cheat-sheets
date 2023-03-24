# Flask Save Images
Class: <a href=""> </a>

Subject: #

Date: 2023-03-24

Topics: #, #, # 

---

# Upload Images - Form

```python
class PictureForm(FlaskForm):
    picture = FileField('Photo', validators=[
        FileRequired(), 
        FileAllowed(['jpg', 'png'], 'Images Only!')
    ])
    submit = SubmitField('Update')
```

# Upload Images - Form HTML 
```python
<form action="" method="post" enctype="multipart/form-data">
    ... {# your csrf token and all fields here #}
</form>
```

# Upload Images - Schema
```python
class User(db.Document, UserMixin):
	# User fields ...
    profile_pic = db.ImageField()
```

# Upload Images to MongoDB

```python
@app.route('/account', methods=['GET', 'POST'])
def account():
    picture_form = PictureForm()
    if picture_form.validate_on_submit():
        img = picture_form.picture.data
        filename = secure_filename(img.filename)
        content_type = f'images/{filename[-3:]}'

        if current_user.profile_pic.get() is None:
            current_user.profile_pic.put(img.stream, content_type=content_type)
        else:
            current_user.profile_pic.replace(img.stream, content_type=content_type)
        current_user.save()
        return redirect(url_for('account'))
    return render_template(...)
```


# Displaying Images Saved on MongoDB
- Assume that we want to show the profile picture of the current_user somewhere on the page.    
- We can read the image data, turn this into a BytesIO object, encode the image in base64, decode this, and display it
```python
def get_b64_img(username):
    user = User.objects(username=username).first()
    bytes_im = io.BytesIO(user.profile_pic.read())
    image = base64.b64encode(bytes_im.getvalue()).decode()
    return image
```

- Example in a route
```python
@app.route("/user/<username>")
def user_detail(username):
	...
	# if found, pull reviews from this username and pass to the rendertemplate
	if user is not None:
		...
		image = get_b64_img(username)
		...
	return render_template( ... , image=image)
```

- Example in HTML
```python
<img class="pic" src="data:image/png;base64,{{image}}" alt="image">
```