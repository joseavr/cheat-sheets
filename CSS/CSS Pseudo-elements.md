# 🎨 CSS Pseudo-elements
Class: <a href="https://github.com/lamula21/cheat-sheets/blob/main/css/CSS.md">CSS</a>

Subject: [[CSS]]

Date: 2023-03-23

Topics: #, #, # 

---
# 🎬 Intro to Pseudo-Elements
A CSS pseudo-element is used to style specified parts of an element.

For example, it can be used to:
- Style the first letter, or line, of an element
- Insert content before, or after, the content of an element
- These pseudo-elements are useful for creating decorative content, such as icons, images, borders, and other visual elements.

# 1️⃣ `::before` & `::after` 
- creates a new `content` (text or other graphical elements) before or after the content of the element selected.
```css
a::before { 
  content: "<"; 
  margin-right: 5px; 
}

a::after { 
  content: ">"; 
  margin-left: 5px; 
}

```


# 2️⃣ `::first-line` & `::first-letter`
- Styles the first line or first letter of an element. 
- For example, you can use them to make the first letter of a paragraph larger or to add a different color to the first line of a heading.
```css
h1::first-letter {
  font-size: 3em;
  color: red;
}

p::first-line {
  font-weight: bold;
  color: blue;
}
```


# 3️⃣ `::selection`
- Styles text that has been selected by the user. 
- For example, you can use it to change the background color of selected text.
```css
::selection {
  background-color: yellow;
}
```


# 4️⃣ `::placeholder`
- Styles the placeholder text of an input field.
- For example, you can use it to change the color or font of the placeholder text.
```css
input::placeholder {
  color: gray;
  font-style: italic;
}
```