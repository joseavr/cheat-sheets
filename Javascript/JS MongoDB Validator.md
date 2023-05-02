# JS MongoDB Express-Validator

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-04-30

---

# 🎬 Intro to Express-Validator

Provides many validation functions that you can use to validate different types of input (forms)

Here are some examples:
- `body()`: This method is used to validate data from the request body. It provides many methods like `isEmail()`, `isInt()`, `isString()` etc. to validate different types of data.
- `param()`: This method is used to validate data from the route parameters.
- `query()`: This method is used to validate data from the query string.
- `header()`: This method is used to validate data from the request headers.
- `cookie()`: This method is used to validate data from cookies.
- `custom()`: This method is used to define custom validation logic. You can pass a function to this method that will receive the input value and can return a boolean or a Promise.

```js
// Validate email address
body('email').isEmail().withMessage('Email address is invalid')

// Validate integer input
body('age').isInt({ min: 18, max: 65 }).withMessage('Age must be between 18 and 65')

// Validate string input
body('username').isString().withMessage('Username must be a string')

// Validate route parameter
param('id').isInt().withMessage('Invalid ID')

// Validate query string
query('page').isInt({ min: 1 }).withMessage('Invalid page number')

// Validate request header
header('Authorization').isJWT().withMessage('Invalid authorization token')

// Define custom validation logic
body('password').custom((value, { req }) => {
  if (value !== req.body.confirmPassword) {
    throw new Error('Passwords do not match');
  }
  return true;
})
```

# Chaining Validations
You can also chain these methods to create complex validation rules,

```js
// Validate a password field that must be at least 8 characters and contain a number
body('password')
  .isLength({ min: 8 })
  .withMessage('Password must be at least 8 characters')
  .matches(/\d/)
  .withMessage('Password must contain at least one number')

// Validate an email field that must be a valid email and have a length of at most 100 characters
body('email')
  .isEmail()
  .withMessage('Email address is invalid')
  .isLength({ max: 100 })
  .withMessage('Email address must be at most 100 characters')

// Validate a name field that must be a string and have a length of at least 2 characters, and at most 50 characters
body('name')
  .isString()
  .withMessage('Name must be a string')
  .isLength({ min: 2, max: 50 })
  .withMessage('Name must be between 2 and 50 characters')

// Validate a date field that must be a valid date and be after a given date
body('date')
  .isDate()
  .withMessage('Invalid date format')
  .isAfter('2022-01-01')
  .withMessage('Date must be after January 1, 2022')

```


# Custom Validations
You can also create your own custom validators using `custom()`.
```js
// Validate that a username is not already taken in the database
body('username')
  .custom(async (value) => {
    const user = await User.findOne({ username: value });
    if (user) {
      throw new Error('Username is already taken');
    }
  })

// Validate that a password contains at least one uppercase letter, one lowercase letter, and one number
body('password')
  .custom((value) => {
    if (!/[A-Z]/.test(value)) {
      throw new Error('Password must contain at least one uppercase letter');
    }
    if (!/[a-z]/.test(value)) {
      throw new Error('Password must contain at least one lowercase letter');
    }
    if (!/\d/.test(value)) {
      throw new Error('Password must contain at least one number');
    }
    return true;
  })

// Validate that a date is within a certain range
body('date')
  .custom((value) => {
    const date = new Date(value);
    const minDate = new Date('2022-01-01');
    const maxDate = new Date('2022-12-31');
    if (date < minDate || date > maxDate) {
      throw new Error('Date must be between January 1, 2022 and December 31, 2022');
    }
    return true;
  })
```

- Custom validation logic using a callback function passed to the `custom()` method.
- This function receives the input value as its first argument, and an options object as its second argument that contains information about the request and response objects.

- If the custom validation function encounters an error, it should throw an instance of `Error` or a string containing the error message.
- If the validation function runs successfully, it should return a truthy value (usually `true`) to indicate that the validation passed.

- You can use `async`/`await` in your custom validation function to perform asynchronous validation, such as querying a database or making an API call. 
- Just make sure to return a Promise from the function.
```js
const { body } = require('express-validator');
const User = require('../models/user');

// Validate that the email address is not already registered
body('email')
  .custom(async (value) => {
    const user = await User.findOne({ email: value });
    if (user) {
      throw new Error('Email address is already registered');
    }
  });
```