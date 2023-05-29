# Title
Adding Form and request/route validations

## Description
In this assignment, you would be building APIs which will have validations for the payload being sent. 

```
...
app.post('/register',
    body("password").isStrongPassword({
        minLength: 8,
        minLowercase: 1,
        minUppercase: 1,
        minNumbers: 1
    })
    .withMessage("Password must be greater than 8 and contain at least one uppercase letter, one lowercase letter, and one number"),
    (req, res) => {
        // Validate incoming input
    })
...
```

Validations allow us to maintain data quality and consistency. Use this link for reference - [Validations in express](https://stackabuse.com/form-data-validation-in-nodejs-with-express-validator/)

## Assignment:

Topic: Adding Validators on Routes in Express

Objective: To learn how to implement validators on routes in Express to ensure proper validation of user input data.

Steps:

1. Install Express and Express Validator: The first step is to install the required packages for Express and Express Validator. Use the following command to install these packages:

```
npm install express express-validator
```

2. Import Required Packages: After installing the packages, import the required packages in your server.js or app.js file:

```javascript
const express = require('express');
const { check, validationResult } = require('express-validator');
```

3. Implement Validators on Routes: Now, you can add validators on your Express routes. For example, if you want to validate the data submitted through a contact form, you can use the following code:

```javascript
app.post('/contact', [
    check('name').notEmpty().withMessage('Name is required'),
    check('email').isEmail().withMessage('Email is invalid'),
    check('message').notEmpty().withMessage('Message is required')
], (req, res) => {
    // Handle form data and validation errors
});
```

In the above code, we have used the `check` function of Express Validator to add validators for `name`, `email`, and `message` fields. The `notEmpty` validator checks if the field is not empty, and the `isEmail` validator checks if the email field is a valid email address. If any of the validators fail, the `withMessage` function sends an error message to the client.

4. Handle Validation Errors: After adding validators, you need to handle validation errors. You can use the `validationResult` function of Express Validator to get the validation errors and send them to the client. Here's an example of how you can handle validation errors:

```javascript
app.post('/contact', [
    check('name').notEmpty().withMessage('Name is required'),
    check('email').isEmail().withMessage('Email is invalid'),
    check('message').notEmpty().withMessage('Message is required')
], (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
        return res.status(422).json({ errors: errors.array() });
    }
    // Handle form data
});
```

In the above code, we have used the `validationResult` function to get the validation errors. If there are any errors, we send them to the client with a 422 status code. If there are no errors, we can handle the form data.

Conclusion:

By following these steps, you can easily implement validators on your Express routes to ensure that the user input data is properly validated. This helps to prevent security issues and improve the overall user experience.


