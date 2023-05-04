# 🎨 CSS Types of Selectors

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 0101

🗓️Date: 2023-02-06

---

# 👉 Selectors
- Useful in CSS to select specific or multiple tags in our HTML for styling
```html
<div class="parent child"> 
  <p id="mi_id_unico">Lorem ipsum dolor sit amet</p>
</div> 

<div class="parent"> 
  <!-- More tags --> 
</div>
```

## HTML Tags Selector
- Select all elements with a tag (`p`)
```css
p {
	text-align: center;
	color: red;
}
```

## ID Selector
- Select a HTML tag by an unique ID (`#`)
```css
#mi_id_unico {
  text-align: center;
  color: red;
}
```

## Class Selector
- Target elements by a class name (`.`)
```css
.parent {
  /* Style */
}
```

- Target a tag with nested class name
```css
<div class="parent child"></div>

.parent.child {
  /* Style */
}
```

## Descendant Selector
- Given HTML
```html
<div class="parent"> 
  <div class="subparent"> 
    <h2 class="text"> Selected </h2>
  </div>
</div> 

<div class="stuff"> 
  <div class="subparent"> 
    <h2 class="text"> No Selected </h2>
  </div>
</div> 
```

- Select a tag that are only descendants of a parent class
```css
.parent .text {
  /* Style */
}
```

- Select a tag that are direct children of a parent class
```css
.parent > .subparent {
  /* Style */
}

.parent > .text {
  /* No selected */
}
```

## Child Selector
- Useful when want to select without changing the HTML file with `classes` selectors
```css
/* p has to be a immeadiate child of body */
body > p { line-height: 1.3 }
```

## Attribute Selector
- Select a tag by an attribute
- Works as a boolean
```html
<a href="http://www.umd.edu" title="news">News</a>
```

```css
a[title="news"] {
	color: red
}
```

## Universal Selector
- Select all tags with a `*` symbol
```css
p * {
	color: red;
}
```