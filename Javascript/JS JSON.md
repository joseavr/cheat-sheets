# JS JSON

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-04-03

---
# 🎬 Intro to JSON

# Understanding JSON Syntax

As the JSON structure is based on the JavaScript object literal syntax, they share a number of similarities.

These are the core elements of JSON syntax:
-   Data is presented in **key**/**value** pairs.
-   Data elements are separated by commas.
-   Curly brackets **{}** determine objects.
-   Square brackets **[]** designate arrays.

As a result, JSON object literal syntax looks like this:
```js
{
   “key”:“value”,
   “key”:“value”,
   “key”:“value”
}
```

Complex JSON
```js
{
  "className":"Class 2B",
  "year":2022,
  "phoneNumber":null,
  "active":true,
  "homeroomTeacher":{"firstName":"Richard", "lastName":"Roe"},
  "members":[
    {"firstName":"Jane","lastName":"Doe"},
    {"firstName":"Jinny","lastName":"Roe"},
    {"firstName":"Johnny","lastName":"Roe"},
  ]
}
```

# What to Choose
When it comes to storing data, JSON offers two methods to do it:
-   **Objects.** This method starts and ends with curly brackets and has two or more key/value pairs with commas separating them. A colon follows each key to distinguish it from the associated value.
-   **Arrays.** This method employs square brackets enclosing the elements with commas separating them.


# Difference between JSON and JS Object
- Main difference is that the key in JSON always is a string - enclosed by `""`
```js
JS Object
{
   key:“value”,
   key:“value”,
   key:“value”
}

JSON
{
   “key”:“value”,
   “key”:“value”,
   “key”:“value”
}
```



