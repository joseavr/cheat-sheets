# React Hooks

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-05-26

---

# React Hooks
- React version 16.8, allows use `state` and other React features without writing a class.
- Provides a way to manage logic and reuse code in functional components.
- There are many react hooks for different situations and utilities.

## `useState()` 
- `useState()`, built-in hook in React, is used keep track of changing data within your components. For example,
	- used to store form input values,
	- toggle buttons, 
	- display dynamic content, or 
	- manage any other stateful data. 
	- Any changes will update the component and re-render the new `state`, ensuring that the UI stays in sync with the data.
- `useState()` takes an initial argument: **boolean**, **array**, **integer**, **string**, **object**.
- Returns an array with two elements: 
	- the current state value 
	- function to update the state

```js
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // defining State

  const increment = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```


## `useRef()` 
- Hook that allows creating mutable reference that persist across the component's lifecyle (similar to a mutable variable in Rust)
- Will not cause a re-render when it changes.
- Useful for storing any value that can mutate, such as identifier, DOM element, counter, etc

### useRef vs useState
- when UI is modified, `useRef()` does not trigger a re-render of the component 
- when UI is modified, `useState()` triggers a re-render of the component

- Here an example
```jsx
import React, { useRef } from 'react';

function ExampleComponent() {
  const inputRef = useRef(null);

  const handleButtonClick = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={handleButtonClick}>Focus Input</button>
    </div>
  );
}
```

## `useEffect()`


## `useTransition()`
Improve performance by reducing the number of re-renders and DOM updates.

Use `startTransition` when you have a section of code that may cause multiple updates to occur, and you want to batch those updates together to improve performance. 

Batching refers to the process of queuing up state updates and re-renders to be executed in a single batch, rather than executing them one by one.



```jsx
function onSubmit(data: Inputs) {
    if (!isLoaded) return

    startTransition(async () => {
      try {
        const result = await signIn.create({
          identifier: data.email,
          password: data.password,
        })

        if (result.status === "complete") {
          await setActive({ session: result.createdSessionId })

          router.push(`${window.location.origin}/`)
        } else {
          /*Investigate why the login hasn't completed */
          console.log(result)
        }
      } catch (error) {
        const unknownError = "Something went wrong, please try again."

        isClerkAPIResponseError(error)
          ? toast.error(error.errors[0]?.longMessage ?? unknownError)
          : toast.error(unknownError)
      }
    })
  }

```

## `useCallback()`

## `useId()`

## `useContext()`

## `useMemo()`: an alterniative for useContext

## zustand??

## `useReducer()`

