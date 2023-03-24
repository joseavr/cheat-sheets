# 🎬 Flask Error Pages
Class: <a href=""> </a>

Subject: [[Flask]]

Date: 2023-03-24

Topics: #, #, # 

---

# 🎬 Intro to Error Pages
- Something causes an error  
- Instead of the default error messages, display our own

# Setup
- Very similar to routes
- No extra imports
- **Important**: use decorator `@app.errorhandler('''error code as an int''')`
	- e.g 404, 500, etc
- View function - Pass any parameter such as `e`  
- Return rendered template AND error code (separated by comma)
- View function can be any name (avoid duplicates)
```python
@app.errorhandler(404)
def error404(e):
    return render_template('template.html'), 404
```

- Every time an user goes to a unknown route, the error page will display