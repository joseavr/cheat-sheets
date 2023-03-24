# Flask Bootstrap
Class: <a href=""> </a>

Subject: #

Date: 2023-03-24

Topics: #, #, # 

---
# Intro
- CSS/JS framework, makes websites look prettier
- We won’t be going over the entire framework (there’s too much), so the documentation is your friend
- Flask-Bootstrap extension is kinda old
- Outdated (last released January 2017), and not really being actively worked on
- Might be too complicated for our use cases, anyway
- Include links to the Content Delivery Network (CDN) in your base.html template file, like how we did for project 3, or…
- This is the recommended method, because browser can cache the framework files for faster reloading when visiting other sites using the same links
- Download from [getbootstrap.com](https://getbootstrap.com/)
- Increases size of your web app, but not reliant on network stability

# Favicons
- Save in static directory as favicon.ico
- Add link tag to between the `<head>` tags
- **<link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}">**

# Alerts


