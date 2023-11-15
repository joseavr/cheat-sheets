# Untitled

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-07-26

---

# Cool Effects

## Blurring an Element

Use `backdrop-blur{amount}` to blur elements, buttons, links, etc.

```html
<a
	class="inline-block border-white bg-white/5 backdrop-blur-3xl 
	 border-[3px] rounded px-20 py-2 font-normal text-sm text-white 
	 hover:bg-white hover:text-black transition-colors">
	 Demo button blurred
</a>
```


# Scrolling Slider Effect

`snap-y snap-mandatory` enables vertical scrolling on the container over children elements. `overflow-auto` allows scrolling when elements overflows. For scroll snapping to work, need to also set `snap-center` on the children elements.

```jsx
<main class="relative w-full h-screen snap-y snap-mandatory overflow-auto">
	<div class="snap-center"><HeroSection /></div>
	<div class="snap-center"><HeroSection /></div>
	<div class="snap-center"><HeroSection /></div>
	<div class="snap-center"><HeroSection /></div>
</main>
```