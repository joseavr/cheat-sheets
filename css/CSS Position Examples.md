# 🎨 CSS Position Examples
Class: <a href="https://github.com/lamula21/cheat-sheets/blob/main/css/CSS.md">CSS</a>

Subject: [[CSS]]

Date: 2023-03-23

Topics: #, #, # 

---

# Modal Window
```css
.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 400px;
  background-color: #fff;
  padding: 20px;
  z-index: 2;
}

.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 1;
}
```


# Sticky Nav Bar
```css
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  background-color: #333;
  color: #fff;
  padding: 10px;
  z-index: 1;
}

.content {
  margin-top: 50px;
}
```

# Simple Tooltip
```css
.button {
  position: relative;
}

.tooltip {
  position: absolute;
  top: -20px;
  left: 50%;
  transform: translateX(-50%);
  background-color: #333;
  color: #fff;
  padding: 5px;
  border-radius: 5px;
  opacity: 0;
  transition: opacity 0.3s;
}

.button:hover .tooltip {
  opacity: 1;
}
```