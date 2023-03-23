# 🎨 CSS Center an Element
Class: <a href="https://github.com/lamula21/cheat-sheets/blob/main/css/CSS.md">CSS</a>

Subject: [[CSS]]

Date: 2023-03-23

Topics: #, #, # 

---

# Center a `<div>`
```css
#MyDialog{
  position:fixed;
  left: 50%;
  top:50%;
  transform: translate(-50%, -50%);
  width: xxx;  /* Any width */
  height: xxx; /* Any height */
}
```


# Align Text in a `<div>`

To align text tags to the left of their respective "div" containers, you can use the following CSS:
```css
.card.movie-info {
  display: flex;   
  justify-content: flex-start;   
  align-items: center; 
} 
.card-title, .card-text {   
  margin: 0;   
  text-align: left; 
}
```

Explanation:
- `display: flex` property makes the "div" container a flex container. 
- `justify-content: flex-start` property aligns the content (text) to the left of the container. 
- `align-items: center` property centers the items vertically in the container (child elements displayed into rows).

- `text-align: left` property aligns the text to the left of the container, and the 
- `margin: 0` property removes any default margins that might be applied to the elements.

# `transform`: Move Element 
- CSS property to apply transformation of an element.
- Can be applied in two-dimensional or three-dimensional space, which includes
	- `scale()`
	- `rotate() `
	- `skew()`
	- `translate()`

- For example, to apply horizontal translation of -20 pixels, which will move it to the left by 20 pixels.
```css
/* Move 20 pixeles to left */
.move-20-px { 
  transform: translateX(-20px); 
}

/* Rotate 45 degrees */
.rotate-45 {
  transform: rotate(45deg);
}

/* Scale an element by a factor of 1.5 */
.scale-up {
  transform: scale(1.5);
}

/* Skew an element by 30 degrees in the x direction */
.skew-x {
  transform: skewX(30deg);
}

/* Translate an element 50 pixels to the right and 20 pixels down */
.translate {
  transform: translate(50px, 20px);
}
```