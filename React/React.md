# React

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-06-28

---

# Intro to React
- No more Vanilla Javascript (Imperative Language) telling Javascript how to do with steps. Instead React offers a Declarative Language, which is telling JS to get the results straight.
- The name "React" because it **reacts** to the changes of the `state` from Hooks and these changes are updated in the UI.
- Uses Virtual DOM. Reacts modifies specific elements in the DOM without using imperative language
- There are 2 ways React updates the UI
	- when `state` of an element is changed, the speficic element is modified and re-rendered
	- when a parent element's `state` is changed, ALL children elements are re-rendered even if some children were not modified


# React Based on Components
- Are functions that return HTML elements
- Used to create user interfaces
- Reusable and independent pieces of code that encapsulate the logic, structure, and styling of a specific part of the UI
```jsx
import React from 'react';

function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}

export default Welcome;
```

# Fragment
- Not allowed to return more than one HTML element in the component
- Return either a single `div` or `Fragment` containing all HTML elements
```jsx
import React, { useState, Fragment } from 'react'; //importing fragment

function Counter() {
	...
  return (
    <Fragment>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </Fragment>
  );
}
```

- Alternative, working on .jsx files can use `<>`
```jsx
function Counter() {
	...
  return (
    <>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </>
  );
}
```

# Properties (Props)
- Pass properties such as data from parent components to child components 
- Use this props in the child components to display in the UI
- Props can be data such as: string, ints, boolean, objects, **functions** (important) 
- Pass props as an *attribute* and values with `{}` enclosed such as: 
	- Variables: `<Greeting name={name} />`
	- Expressions: `<Greeting age={currentYear - birthYear} />`
	- Functions Calls: `<Greeting message={getMessage()} />`
	- Conditionals Expressions: `<Greeting isLoggedIn={isLoggedIn ? true : false} />`
	- Objects: `<Person info={{ name: 'John', age: 30 }} />`
	- Something that returns data
- To use Props in child components, use the parameter with enclosed `{}`
	- *Note: Props are immutable, DO NOT modify them*
```jsx
// Parent component: App.js
function App() {
  const name = 'John';

  return (
    <div>
      <Greeting nameProp={name} /> {/* Passing prop here */}
    </div>
  )
}

// Child component: Greeting.js
function Greeting( {nameProp} ) {     // Using Prop in Children component
  return <h1>Hello, {nameProp}!</h1>;
}
```

## Passing HTML Elements
- Can also pass elements to the props
```jsx
// Parent component: App.js
function App() {
  const html = <span>Jhon!</span>; // HTML Element
	
  return (
    <div>
      <Greeting htmlProp={html} /> {/* Passing prop here */}
    </div>
  );
}

// Child component: Greeting.js
function Greeting({htmlProp}) {     // Using Prop in Children component
  return <h1>Hello, {htmlProp}</h1>;
}
```

## Children 
- Can also encapsulate a element to pass another elements, called as childrens
- Must use `children` in the child component function paramenter
```jsx
// Parent component: App.js
export const App = () => {  
	return (
		<TwitterCard> 
			{/* Passed as children */}
			<h1> Jose Valdivia </h1>
			More elements here...
		</TwitterCard>
	)
}

// Child component: TwitterCard.jsx
export const TwitterCard = ({ children }) => {	
	return (
		<strong>{children}</strong>
	)
}
```

## Props Drilling

