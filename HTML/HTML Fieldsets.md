# HTML FieldSets

📚Class: CMSC 335 Javascript & Web Dev

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/">HTML</a>

✏️Section: 0101

🗓️Date: 2023-05-06

---

# FieldSets
- `fieldset` tag groups related form fields together 
- `legend` tag provides a caption or title for the group. 
- The `label` tags provide labels for each form field, which are associated with the `id` attribute of the corresponding `input` tag using the `for` attribute. Allows screen readers to read out the labels when the user interacts with the form.
- The `input` tags are used to create form fields where users can input data.
- Each input field has a `type` attribute, which specifies the type of input that is expected, and a `name` attribute, which is used to identify the input field when the form is submitted.
- The `br` tags are used to create line breaks, which are used here to separate the form fields and make the form more readable.

```html
<form>
  <fieldset>
    <legend>Personal Information</legend>
    
    <label for="name">Name:</label>
    <input type="text" id="name" name="name"><br><br>
    
    <label for="email">Email:</label>
    <input type="email" id="email" name="email"><br><br>
    
    <label for="phone">Phone:</label>
    <input type="tel" id="phone" name="phone"><br><br>
  </fieldset>
</form>
```

