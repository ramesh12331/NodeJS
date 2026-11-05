# 📘 PART 6 — REST API DEVELOPMENT

# Chapter 25 — REST API Validation



Beginner Level

Practical Examples



## 📚 Chapter Topics

In this chapter, we will learn:

1. What is API Validation?
2. Why do we need validation?
3. Real-world example
4. Validation flow
5. Types of validation
6. Required field validation
7. String validation
8. Number validation
9. Email validation
10. Custom validation middleware
11. Express-validator
12. Practical Student API
13. Common mistakes
14. Best practices
15. Interview questions
16. Practice problems
17. Mini challenge
18. Chapter summary

## 1. What is API Validation?

API Validation means checking incoming user data before processing or saving it.

For example, imagine a student registration API.

The user sends:

```
{
    "name": "Ramesh",
    "age": 25,
    "course": "Node.js"
}
```

This data is valid.

But what happens if the user sends:

```
{
    "name": "",
    "age": -10,
    "course": ""
}
```

This data is invalid because:

- Name is empty.
- Age is negative.
- Course is empty.

Validation helps us reject incorrect data.

## 2. Why do we need API Validation?

Without validation, users can submit incorrect data to our backend.

For example:

| Field  | Valid data        | Invalid data |
| ------ | ----------------- | ------------ |
| Name   | Ramesh            | Empty string |
| Age    | 25                | -10          |
| Email  | ramesh\@gmail.com | ramesh123    |
| Course | Node.js           | Empty string |
| Price  | 500               | -100         |

We use validation to:

- Prevent incorrect data.
- Maintain database quality.
- Improve application security.
- Give clear error messages.
- Avoid application errors.

## 3. Real-world example

Imagine an online shopping application.

When a user adds a product, the API receives:

```
{
    "name": "Laptop",
    "price": 50000,
    "stock": 10
}
```

Our backend should check:

1. Is the product name provided?
2. Is the price a positive number?
3. Is stock a valid non-negative integer?

If everything is correct, save the product.

Otherwise, return an error.

## 4. API Validation Flow

```
        CLIENT / POSTMAN
                |
                v
          Send JSON Data
                |
                v
          EXPRESS SERVER
                |
                v
          VALIDATION
                |
          +-----+-----+
          |           |
        Valid       Invalid
          |           |
          v           v
      Controller    Return 400
          |         Error Message
          v
      Save Data
          |
          v
      Return Success
```

Remember: Validation should happen before saving data.

## 5. Types of Validation

Common validation types:

| Validation | Purpose                             |
| ---------- | ----------------------------------- |
| Required   | Check whether a field exists        |
| String     | Check whether the value is a string |
| Number     | Check whether the value is numeric  |
| Email      | Check email format                  |
| Length     | Check minimum and maximum length    |
| Range      | Check minimum and maximum values    |
| Custom     | Apply our own business rules        |

There is also a related concept called sanitization.

- Validation checks whether data is acceptable.
- Sanitization cleans or normalizes data.

Example:

```
const name = "  Ramesh  ";

const cleanName = name.trim();

console.log(cleanName);
```

Output:

```
Ramesh
```

`trim()` removes spaces from the beginning and end.

## 6. Required Field Validation

A required field means the user must provide a value.

Example:

```
const name = "Ramesh";
const course = "Node.js";

if (!name || !course) {
    console.log("Name and course are required");
} else {
    console.log("Valid data");
}
```

Output:

```
Valid data
```

### Express API example

```
app.post("/students", (req, res) => {

    const { name, course } = req.body;

    // Check required fields
    if (!name || !course) {
        return res.status(400).json({
            message: "Name and course are required"
        });
    }

    res.status(201).json({
        message: "Student data is valid"
    });

});
```

Important: `return` prevents the function from continuing after sending an error response.

## 7. String Validation

Sometimes we need to check whether the input is a string.

```
const name = "Ramesh";

// Check string type
if (typeof name !== "string") {
    console.log("Name must be a string");
} else {
    console.log("Valid name");
}
```

Output:

```
Valid name
```

### Check empty strings

```
const name = "   ";

if (typeof name !== "string" || name.trim() === "") {
    console.log("Name cannot be empty");
} else {
    console.log("Valid name");
}
```

Output:

```
Name cannot be empty
```

Why use `trim()`?

Because `"   "` contains spaces but does not contain a meaningful name.

## 8. Number Validation

Suppose the user provides an age.

Valid age:

```
const age = 25;
```

Invalid age:

```
const age = -10;
```

### Example

```
const age = 25;

// Check integer and positive value
if (!Number.isInteger(age) || age <= 0) {
    console.log("Age must be a positive integer");
} else {
    console.log("Valid age");
}
```

Output:

```
Valid age
```

You can also set a maximum:

```
if (!Number.isInteger(age) || age < 1 || age > 120) {
    console.log("Enter a valid age");
}
```

Important: Avoid using only `!age` to check numbers. Zero is also treated as falsy in JavaScript. Use explicit checks such as `age === undefined` or `Number.isInteger(age)`.

## 9. Email Validation

An email should follow a recognizable email format.

Valid example:

```
ramesh@gmail.com
```

Invalid example:

```
ramesh123
```

For a simple learning example:

```
const email = "ramesh@gmail.com";

// Simple email format check
const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

if (!emailPattern.test(email)) {
    console.log("Invalid email");
} else {
    console.log("Valid email");
}
```

Output:

```
Valid email
```

This regular expression is only a basic format check. Real email validation is more complex, so using a validation library is usually better.

## 10. Custom Validation Middleware

In Express, we can create our own validation middleware.

Middleware checks the request data before the controller executes.

### Project structure

```
student-api/
│
├── middleware/
│   └── validateStudent.js
│
├── controllers/
│   └── studentController.js
│
├── routes/
│   └── studentRoutes.js
│
└── server.js
```

### Step 1: Create `validateStudent.js`

```
// Custom validation middleware

const validateStudent = (req, res, next) => {

    // Get data from request body
    const { name, age, course } = req.body;

    const errors = [];

    // Validate name
    if (typeof name !== "string" || name.trim() === "") {
        errors.push("Name is required");
    }

    // Validate age
    if (!Number.isInteger(age) || age < 1 || age > 120) {
        errors.push("Age must be a valid positive integer");
    }

    // Validate course
    if (typeof course !== "string" || course.trim() === "") {
        errors.push("Course is required");
    }

    // If errors exist, return response
    if (errors.length > 0) {
        return res.status(400).json({
            success: false,
            errors: errors
        });
    }

    // Continue to next middleware or controller
    next();
};

module.exports = validateStudent;
```

### Step 2: Create `studentController.js`

```
const students = [];

const createStudent = (req, res) => {

    const { name, age, course } = req.body;

    const newStudent = {
        id: students.length + 1,
        name: name.trim(),
        age,
        course: course.trim()
    };

    students.push(newStudent);

    res.status(201).json({
        message: "Student created successfully",
        data: newStudent
    });

};

module.exports = {
    createStudent
};
```

### Step 3: Create `studentRoutes.js`

```
const express = require("express");

const router = express.Router();

const validateStudent = require("../middleware/validateStudent");

const { createStudent } = require("../controllers/studentController");

// Validation runs before controller
router.post("/", validateStudent, createStudent);

module.exports = router;
```

### Step 4: Create `server.js`

```
const express = require("express");

const app = express();

// Read JSON request data
app.use(express.json());

// Import routes
const studentRoutes = require("./routes/studentRoutes");

// Register routes
app.use("/api/students", studentRoutes);

// Start server
app.listen(3000, () => {
    console.log("Server running on port 3000");
});
```

### How does this work?

```
POST /api/students
        |
        v
   express.json()
        |
        v
 validateStudent
        |
        +----------+
        |          |
      Invalid     Valid
        |          |
        v          v
     400 Error  createStudent
                   |
                   v
               Save Student
                   |
                   v
               201 Response
```

## 11. Express-validator

So far, we have written validation manually.

But in real projects, we can use a package called express-validator.

It provides ready-made validation functions.

### Step 1: Install package

Open the VS Code terminal:

```
npm install express-validator
```

### Step 2: Import functions

```
const { body, validationResult } = require("express-validator");
```

- `body()` validates request body fields.
- `validationResult()` collects validation errors.

### Step 3: Create validation rules

```
const { body, validationResult } = require("express-validator");

const validateStudent = [

    // Name validation
    body("name")
        .trim()
        .notEmpty()
        .withMessage("Name is required"),

    // Course validation
    body("course")
        .trim()
        .notEmpty()
        .withMessage("Course is required"),

    // Age validation
    body("age")
        .isInt({ min: 1 })
        .withMessage("Age must be a positive integer"),

    // Email validation
    body("email")
        .isEmail()
        .withMessage("Enter a valid email"),

    // Check validation errors
    (req, res, next) => {

        const errors = validationResult(req);

        if (!errors.isEmpty()) {
            return res.status(400).json({
                errors: errors.array()
            });
        }

        next();
    }

];

module.exports = validateStudent;
```

### Step 4: Use validation in routes

```
const express = require("express");

const router = express.Router();

const validateStudent = require("../middleware/validateStudent");

const { createStudent } = require("../controllers/studentController");

router.post("/", validateStudent, createStudent);

module.exports = router;
```

Remember: The validation middleware runs before `createStudent`.

## 12. Practical Student API — Postman Testing

Let's test our API.

### Valid request

Expected: 201 Created

Method: POST

URL:

```
http://localhost:3000/api/students
```

Body → raw → JSON:

```
{
    "name": "Ramesh",
    "age": 25,
    "course": "Node.js",
    "email": "ramesh@gmail.com"
}
```

Expected response:

```
{
    "message": "Student created successfully",
    "data": {
        "id": 1,
        "name": "Ramesh",
        "age": 25,
        "course": "Node.js"
    }
}
```

### Invalid request

Expected: 400 Bad Request

```
{
    "name": "",
    "age": -10,
    "course": "",
    "email": "invalid-email"
}
```

Expected validation errors:

```
{
    "errors": [
        {
            "msg": "Name is required"
        },
        {
            "msg": "Age must be a positive integer"
        },
        {
            "msg": "Course is required"
        },
        {
            "msg": "Enter a valid email"
        }
    ]
}
```

The exact error objects returned by express-validator can include additional fields such as type, location, path and value.

## 13. Common Validation Mistakes

| Mistake                                    | Correct approach             |
| ------------------------------------------ | ---------------------------- |
| Not checking required fields               | Check every required field   |
| Not using `express.json()`                 | Add JSON middleware          |
| Using only frontend validation             | Validate on backend too      |
| Checking only `!age`                       | Use explicit number checks   |
| Not trimming strings                       | Use `.trim()`                |
| Returning status 200 for invalid data      | Use 400 or 422               |
| Not using `return` after an error response | Use `return res.status(...)` |

## 14. Best Practices

1. Always validate incoming data on the backend.
2. Keep validation rules reusable.
3. Use clear error messages.
4. Check data types and allowed ranges.
5. Trim string inputs when appropriate.
6. Use libraries for complex validation.
7. Never trust data just because frontend validation passed.
8. Do not expose internal server errors to clients.

## 15. Interview Questions

## 16. Practice Problems

Try these small exercises.

- Check whether a username is empty.
- Check whether a password has at least 8 characters.
- Check whether age is between 18 and 60.
- Check whether price is greater than zero.
- Check whether email has a valid format.
- Create a validation middleware for an employee API.

## 17. Mini Challenge — Product API Validation

Try it yourself

Create a Product API with these fields:

```
{
    "name": "Laptop",
    "price": 50000,
    "category": "Electronics",
    "stock": 10
}
```

Requirements:

| Field    | Validation rule      |
| -------- | -------------------- |
| name     | Required string      |
| price    | Positive number      |
| category | Required string      |
| stock    | Non-negative integer |

### Your task

Step 1 — Requirement

Create a validation middleware called `validateProduct`.

Step 2 — Input

```
{
    "name": "",
    "price": -500,
    "category": "",
    "stock": -5
}
```

Step 3 — Expected output

```
{
    "success": false,
    "errors": [
        "Product name is required",
        "Price must be greater than zero",
        "Category is required",
        "Stock must be a non-negative integer"
    ]
}
```

Step 4 — Logic hint

```
Receive product data
       |
       v
Check name
       |
       v
Check price
       |
       v
Check category
       |
       v
Check stock
       |
       v
Are errors present?
       |
    +--+--+
    |     |
   Yes    No
    |     |
    v     v
 Return  Continue
 400     to controller
```

Step 5 — Pseudocode

```
Create validateProduct middleware

Get product fields from req.body

Create empty errors array

If name is invalid:
    Add name error

If price is invalid:
    Add price error

If category is invalid:
    Add category error

If stock is invalid:
    Add stock error

If errors exist:
    Return 400 response

Otherwise:
    Call next()
```

Try writing the middleware yourself. I will review your code and explain any mistakes.

## 18. Chapter Summary

| Concept             | Meaning                          |
| ------------------- | -------------------------------- |
| Validation          | Checking incoming data           |
| Required validation | Checking mandatory fields        |
| String validation   | Checking string values           |
| Number validation   | Checking numeric values          |
| Email validation    | Checking email format            |
| Middleware          | Checks request before controller |
| `next()`            | Moves to next middleware         |
| `express-validator` | Validation library               |
| Sanitization        | Cleaning input data              |

### Quick Revision

- Validation = Check data.
- Sanitization = Clean data.
- Middleware = Check before controller.
- 400 = Bad Request.
- `next()` = Continue execution.

Chapter 25 Completed

Next: Chapter 26 — REST API Testing with Postman

We will learn how to test GET, POST, PUT, PATCH and DELETE APIs, inspect responses, test error cases, and organize API requests into collections.

Type NEXT to start Chapter 26.