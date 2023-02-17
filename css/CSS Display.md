# Display
Class: [[CSS]]
Subject: #
Date: 2023-02-08
Topics: #, #, # 

---

# Display Property

- Type of rendering box
- `display` controls the design of our webpage
- Value:
	- inline
	- block
	- inline-block
	- none
	- flex
	- grid

## Block
- Always start in a new line and occupies all width available
```css
elemento {
    display: block;
}
```

![[Pasted image 20230208172239.png]]

## Inline
- It doesnt start in a new line
- Occupies what is necessary
```css
elemento {
    display: inline;
}
```


# Float Property

## CSS Normal Flow
- Elements are placed one after another on the document structure whether is inline or block

## Float

# Position Property

- Reset position by default from web
```css
* {

	/* Important: to better understanding positioning,

	   we are setting the padding and margin of all

	   elements to zero */

	padding: 0;

	margin: 0;

}
```

## Static
- normal position–no effect
```css
p {

	position: static;  /* By default is relative*/
	
	width: 20rem;

	border-style: solid;



	/* The following has no effect if position:static */
	left: 5rem;

	top: 10rem;

}

```

## Relative 
- Move a element with CSS
- If you make the window smaller, you will see scroll bars
```css
p {

	/*position: static;   By default is relative*/
	position: relative; /* Allows to move a block position*/
	
	width: 20rem;

	border-style: solid;



	/* The following has no effect if position:static */
	left: 5rem;

	top: 10rem;

}
```

## Fixed
- If you make the window smaller, you will NOT see scroll bars
```css
p {

	position: fixed;  /* Allows us*/
	
	width: 20rem;

	border-style: solid;



	/* The following has no effect if position:static */
	left: 5rem;

	top: 10rem;

}
```

## Absolute

- The element will move relative to the parent container. 
- Important:
	- If parent container is static, then it won't be relative to parent container anymore.
```css
p {

	position: absolute; /* Containing block is the body block */

	width: 20rem;

	border-style: solid;



	left: 0rem;

	top: 0rem;

}
```

# Flex Display Property

- Place elements in this container either horizontally or vertically
```css
#container {

	width:40rem;

	height:20rem;

	border: 1rem solid green;

	display: flex; /* Change to block */

	flex-direction: column; /* row is the default, try column. row-reverse */
	flex-direction: row;
	
	align-items: center; /* try center, flex-start, flex-end */
	align-items: flex-end;
	align-items: flex-start;

	justify-content: space-around; /* try space-between */
	justify-content: space-between;

}
```
![[Pasted image 20230208174818.png]]

## Flex vs Grid
![[Pasted image 20230208175436.png]]

