# 🆚 HTML Block vs Inline
Class: [[]]
Subject: #
Date: 2023-03-05
Topics: #, #, # 

---

# Intro 

In HTML, elements are categorized as either block-level or inline-level elements based on how they are displayed in the web page.

#  Block-level elements

- Are displayed as a rectangular block on the web page.
- Occupy the entire width of their parent container by default.
- Allow setting width, height, margin, padding, and border properties.
- Examples include `<div>`, `<p>`, `<h1>` to `<h6>`, `<ul>`, `<ol>`, `<li>`, `<table>`, `<form>`, etc.

# Inline-level elements:

- Are displayed within the text of a paragraph, inline with the surrounding content.
- Only occupy the minimum amount of space necessary to display their content.
- Do not allow setting width, height, top/bottom margins or paddings, and borders.
- Examples include `<span>`, `<a>`, `<img>`, `<strong>`, `<em>`, `<br>`, etc.

# ⛔️ Note
It's worth noting that some elements can be both block-level and inline-level, such as the `<img>` element, which is an inline-level element by default, but can be changed to block-level by adding the CSS property `display: block;`.