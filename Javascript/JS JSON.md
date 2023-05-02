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

# 🆚 Stringify vs Parse
The `JSON.stringify()` method takes a JavaScript object and converts it into a JSON string.
While the `JSON.parse()` method takes a JSON string and converts it into a JavaScript object.

These methods are commonly used for sending and receiving data between web servers and web applications, as JSON is a popular format for data interchange.
```js
// Example object
const myObj = { 
  name: "John",
  age: 30,
  city: "New York"
};

// Converting object to JSON string
const jsonString = JSON.stringify(myObj);
console.log(jsonString);

// Converting JSON string back to object
const parsedObj = JSON.parse(jsonString);
console.log(parsedObj);

```


# 🔄 Iterating a JSON
Suppose we have the following JSON object
```js
const data = {
  id: "2",
  company: "Example Inc.",
  status: "Active",
  notes: "This is a note about the job."
};
```

- For...of iteration (iterating over an array)
```js
for (const [key, value] of Object.entries(data)) {
  console.log(key, value);
}
```

- ForEach iteration
```js
Object.entries(data).forEach(([key, value]) => {
  console.log(key, value);
});
```

- For...in (iterating over the object directly)
```js
for (const key in data) { 
  const value = data[key]; console.log(key, value); 
}
```