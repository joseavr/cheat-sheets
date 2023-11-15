# Untitled

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-07-26

---

# Multiple Selectors

## Select child elements from parent

Use `[...>...>...]` utlities to select child elements. Useful when there are repetetive elements within a parent element

```html
<ul class="[&>li>a]:inline-block [&>li>a]:px-4 [&>li>a]:py-2">
	<li><a href="">Model S</a></li>
	<li><a href="">Model 3</a></li>
	<li><a href="">Model X</a></li>
	<li><a href="">Model Y</a></li>
	<li><a href="">Powerwall</a></li>
	<li><a href="">Carga</a></li>
</ul>
```