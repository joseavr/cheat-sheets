# Flask Models Schema
Class: <a href=""> </a>

Subject: [[Flask]]

Date: 2023-03-23

Topics: #, #, # 

---

# 🎬 Intro to Model Schema
- A Model Schema is a logical structure that defines a `document`, which is stored in a  `collection`. 
- Describes the fields, data types, validations, and other constraints of the `document`s.
- Model Schemas can store differenet fields:
	- Users: name, email, password, age, profilePic, createdAt
	- Reviews: commenter, movie, comment, date
	- Books: buyer, bookName, date
	- Movies: directed, releaseDate, actors, oscarWon

- In flask, a Model Schema is represented as a `Class <document>(db.Document)`
```python
class User(db.Document):
    email = db.EmailField(unique=True, required=True)
    username = db.StringField(unique=True, required=True)
    password = db.StringField()
```

# Building a Schema
- To get started:
```bash
pip3 install flask-mongoengine
```

```python
from flask import Flask
from flask_mongoengine import MongoEngine

app = Flask(__name__)
app.config['MONGODB_SETTINGS'] = {
    'db': 'week_5_database',
    'host': 'mongodb://localhost:27017/',
}
db = MongoEngine(app)
```

## A Simple User Schema
- Since our db is enforce with MongoEngine, we can import Fields such as StringFields, EmailField, etc. (Similar to forms)
- MongoEngine Fields reference: docs.mongoengine.org/apireference.html#fields
```python
from flask_login import UserMixin # To link current_user with this schema
from . import db, login_manager # import db from our __init__

class User(db.Document, UserMixin):
	# username field
	username = db.StringField(unique=True, required=True)
	
	# email field
	email = db.EmailField(unique=True, required=True)
	
	# password field
	password = db.StringField()
	
	# profile_pic field
	profile_pic = db.ImageField()
	
	# dark_mode field
	dark_mode = db.BooleanField(default=False)
	
	# Returns unique string identifying our object
	# Required if we want these properties/methods for current_user
	#.is_authenticated, is_active, is_anonymous. .get_id()
	def get_id(self):
		return self.username
```

## `current_user`
- Since we passed `UserMixin` , links `current_user` with this schema
- Means that we can use ALL properties/methods `User` class may have
	- current_user.username
	- current_user.email
	- current_user.password
	- current_user.profile_pic
	- current_user.dark_mode
	- current_user.get_id()
- Since we overrided `get_id()`, we can use these properties/methods
	- current_user.is_authenticated
	- current_user.is_active
	- current_user.is_anonymous
	- current_user.get_id()
- To make `flask_login` returns the active user, we **MUST** implement:
```python
# in models.py
from flask_app import login_manager
@login_manager.user_loader
def load_user(user_id):
    return User.objects(username=user_id).first()
```
- To make entire app compatible, we **MUST** implement:
```python
# in __init__.py
from flask_login import LoginManager
login_manager = LoginManager(app)
login_manager.login_view = 'login'
```

## Create, Query, Modify, Save Documents
-   To create documents and insert into collections
```python
user = Username(username='Link', email='link@hyrule.org', password=hashed)
user.save() #save user in db
```

-   To query for documents, use User.objects() to retrieve all Users
```python
User.objects(username='Samus') # query for users matching a certain username
User.objects(username=current_user.username).first() # get a single document  
```

-   To update a particular document, use modify()
```python
user = User.objects(username=current_user.username).first() #find user in db
user.modify(username='New username') #modify its fields
user.save() #save in db
```

## A Complex Schema
```python
class Review(db.Document):
	# user field - reference to the User who commented
	commenter = db.ReferenceField(User, required=True)
	
	# content field - with length between 5 and 500 characters
	content = db.StringField(min_length=5, max_length=500, required=True)
	
	# date field - saved as a string instead of a datetime
	date = db.StringField(required=True)
	
	# imdb_id field - with length 9
	imdb_id = db.StringField(min_length=8, max_length=10, required=True)
	
	# movie_title field - with length between 1 and 100 characters
	movie_title = db.StringField(min_length=1, max_length=100, required=True)
```
