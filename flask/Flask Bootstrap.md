# Flask Bootstrap
Class: <a href=""> </a>

Subject: #

Date: 2023-03-24

Topics: #, #, # 

---
# Intro to Bootstrap
- CSS/JS framework, makes websites look prettier
- Import from [getbootstrap.com](https://getbootstrap.com/)

## Documentation
- [Bootstrap Docs](https://getbootstrap.com/docs/5.3/getting-started/introduction/)
- [W3School Bootstrap Tutorial](https://www.w3schools.com/bootstrap/)
- [MD Bootstrap Docs](https://mdbootstrap.com/docs/)

## Why Bootstrap?
Advantages of Bootstrap:
- **Easy to use:** Anybody with just basic knowledge of HTML and CSS can start using Bootstrap
- **Responsive features:** Bootstrap's responsive CSS adjusts to phones, tablets, and desktops
- **Mobile-first approach:** In Bootstrap, mobile-first styles are part of the core framework
- **Browser compatibility:** Bootstrap 5 is compatible with all modern browsers (Chrome, Firefox, Edge, Safari, and Opera). **Note** that if you need support for IE11 and down, you must use either BS4 or BS3.

# Importing Bootstrap to our App
- Include these codes in our HTML file
```html
<!-- Include in <head> -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-aFq/bzH65dt+w6FI2ooMVUpc+21e0SRygnTpmBvdBgSdnuTN7QbdgL+OapgHtvPp" crossorigin="anonymous">
```

```html
<!-- Include at the end of <body> -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha2/dist/js/bootstrap.bundle.min.js" integrity="sha384-qKXV1j0HvMUeCBQ+QVp7JcfGl760yU08IQ+GpUo5hlbpg51QRiuqHAJz8+BrxE/N" crossorigin="anonymous"></script>
```

# Favicons
- Save in static directory as favicon.ico
- Add link tag to between the `<head>` tags
- **<link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}">**

# Bootstrap Icons
- Include this code in `<head>`
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.3/font/bootstrap-icons.css">
```

- Boxicons, similar to Bootstrap icons: [Boxicons Docs](https://boxicons.com/usage)

# Avatar
- [Bootstrap Avatar v5](https://mdbootstrap.com/docs/standard/extended/avatar/)

# Alerts
- [W3Schools Bootsrap Alerts](https://www.w3schools.com/bootstrap/bootstrap_alerts.asp)

# Badges
- [Bootstrap Badges](https://getbootstrap.com/docs/4.0/components/badge/)
- [W3Schools Bootstrap Badges](https://www.w3schools.com/bootstrap/bootstrap_badges_labels.asp)

# Containers

# Carousel
- [Bootstrap Carousel v4](https://mdbootstrap.com/docs/b4/jquery/javascript/carousel/)
- [Bootstrap Carousel v5](https://mdbootstrap.com/docs/standard/components/carousel/)

# Layouts
- [Bootstrap Layout Grid v5](https://mdbootstrap.com/docs/standard/layout/grid/)

# Tables
- [Bootstrap Tables v5](https://getbootstrap.com/docs/5.3/content/tables/)

# Navbar
- [Bootstrap Navbar v5](https://getbootstrap.com/docs/5.3/components/navbar/)

# Cards
- [MD Bootstrap Cards](https://mdbootstrap.com/docs/standard/components/cards/)

# Forms
- [Bootstrap Forms](https://getbootstrap.com/docs/4.4/components/forms/)

# Some Useful Components
- [Bootstrap Extended Components](https://mdbootstrap.com/docs/standard/extended/)