#  🎨 CSS Properties

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 0101

🗓️Date: 2023-03-23

---

# 1️⃣ `transform`: Move Element 
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

# 2️⃣ `z-index:` Wrap behind or front
- CSS property that controls overlap elements on a web page.
- Such as places an element behind or front of other elements
- `z-index` only works on positioned elements (elements with a `position` property value of `absolute`, `relative`, `fixed`, or `sticky`) but not `static`
- For example, In this example, the `div` element has a lower `z-index` value than the `img` element, so the `img` element will appear on top of the `div` element.
```css
div { z-index: 1; }  
img { z-index: 2; }
```

# 3️⃣ `transition` : smoothly animation
- CSS property to smoothly animate changes in CSS property values over a specified duration.
```css
/* Apply a transition to all properties */
transition: <property> <duration> <timing-function> <delay>;

/* Apply a transition to a specific property */
transition-property: <property>;
transition-duration: <duration>;
transition-timing-function: <timing-function>;
transition-delay: <delay>;
```

Explanation:
-   `<property>`: name of the CSS property want to apply the transition to (e.g. `background-color`, `width`, `opacity`, etc.). Use `all` to apply the transition to all properties.
-   `<duration>`: time the transition should take to complete, (e.g. `0.5s`, `200ms`).
-   `<timing-function>`: how the transition progresses over time (e.g. `ease`, `linear`, `ease-in-out`, etc.). Custom timing functions with `cubic-bezier()` function.
-   `<delay>`: time to wait before starting the transition, (e.g. `1s`, `500ms`).


# 4️⃣ `background-color`: Color a div
- Color a `<div>`
- Useful with hover
```css
div:hover {
  background-color: <pick-transparent-color>;
}
```

![](../Assets/20230323155029.png)