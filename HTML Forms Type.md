# 💻 HTML Forms Type
Class: [[HTML/HTML]]
Subject: #
Date: 2023-02-23
Topics: #, #, # 

---


WebServersFormCOde.zip
[AccessFormDataUsingJSCode.zip](https://www.cs.umd.edu/class/spring2023/cmsc335/prot/lectures/Week09/AccessFormDataUsingJSCode.zip)


# 🏷️ Label
- Used to associate with a HTML form tag, `<input>`
- Provides description of what the form box is and is displayed before the text field
```html
<label for="username">Username:</label>
<input type="text" id="username" name="username">
```


# ⌨️ Input Type
- Used for user enters data/information
- There are many input tags with different `types` attributes

## Text Area
- Multi-line text input area for users to enter text
```html
<textarea id="message" name="message" rows="5" cols="30"></textarea>
```

## Checkbox 
- 

## Radio Button

## Scroll Label



## Number Range


## Drop Down List



## Submit


## Reset

## Tel

# 👇 Input Attributes
## Placeholder attribute
https://www.w3schools.com/tags/tryit.asp?filename=tryhtml5_input_placeholder

## Pattern attribute
https://www.w3schools.com/tags/tryit.asp?filename=tryhtml5_input_placeholder

## Required attribute
```html
<label for="max-cost"> <u>Credit Card #</u> </label>
	<input type="text" name="cc1" id="" pattern="[0-9]{4}" required> <br> <br>
	
	<input type="text" name="cc2" id="" pattern="[0-9]{4}" required> <br> <br>
	
	<input type="text" name="cc3" id="" pattern="[0-9]{4}" required> <br> <br>
	
	<input type="text" name="cc4" id="" pattern="[0-9]{4}" required> <br> <br>
```


# Input-List
## Datalist


# Select
```html
<label for="item-category"><u>Item Category</u> </label>

<select name="plan" id="item-category">
	<option value="none" selected disabled hidden></option>
	<option value="free">clothes</option>
	<option value="starter">books </option>
	<option value="professional">music</option>
	<option value="corporate">food</option>
	<option value="corporate">other</option>
</select>
```

![[20230223202341.png]]
