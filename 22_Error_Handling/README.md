# 🚀 PART 5 — EXPRESS.JS

# Chapter 22 — Express Error Handling

BEGINNER LEVEL → PRACTICAL LEVEL

## 📚 Table of Contents

1. What is Error Handling?
2. Why do we need Error Handling?
3. Real-world Analogy
4. Error Handling Flow
5. Types of Errors
6. Basic Error Handling Example
7. `try...catch`
8. `throw new Error()`
9. `next(error)`
10. Error-handling Middleware
11. Practical Example — Student CRUD API
12. HTTP Status Codes
13. Common Mistakes
14. Best Practices
15. Interview Questions
16. Practice Problems
17. Mini Challenge
18. Chapter Summary & Quick Revision

## 1. 🧠 What is Error Handling?

Error handling is the process of identifying, managing, and responding to errors in an application.

In simple words:

Sometimes our API does not work as expected.

For example:

- Student ID does not exist.
- Required data is missing.
- Database connection fails.
- User enters an invalid email.
- Server encounters an unexpected problem.

Instead of crashing or leaving the request hanging, we handle the error and send a meaningful response.

### Example without error handling

```
app.get("/students/:id", (req, res) => {

    const student = students.find(
        (item) => item.id === Number(req.params.id)
    );

    res.json(student);

});
```

What happens if the student does not exist?

The API may return:

```
null
```

This response does not clearly explain the problem.

### Example with error handling

```
app.get("/students/:id", (req, res) => {

    const student = students.find(
        (item) => item.id === Number(req.params.id)
    );

    if (!student) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    res.json(student);

});
```

Now the response is meaningful:

```
{
    "message": "Student not found"
}
```

## 2. 🤔 Why do we need Error Handling?

Imagine you are building a Student Management API.

Your API supports:

```
GET     /students
GET     /students/:id
POST    /students
PUT     /students/:id
DELETE  /students/:id
```

Different problems can happen.

| Situation                 | Error                 |
| ------------------------- | --------------------- |
| Student ID does not exist | Student not found     |
| Name is missing           | Validation error      |
| Invalid ID                | Invalid request       |
| Database is unavailable   | Database error        |
| Unexpected server problem | Internal server error |

### Benefits

1. Prevents unexpected application failures.
2. Gives meaningful error messages.
3. Helps developers debug problems.
4. Improves API reliability.
5. Makes API responses consistent.
6. Helps frontend developers understand what went wrong.

## 3. 🌍 Real-world Analogy

Imagine booking a train ticket.

```
CUSTOMER
   |
   v
REQUEST TICKET
   |
   v
CHECK SEAT AVAILABILITY
   |
   +---- Seat Available
   |          |
   |          v
   |      BOOK TICKET
   |
   +---- No Seat Available
              |
              v
        SHOW ERROR MESSAGE
```

The booking system does not simply stop working when no seats are available.

It displays a meaningful message.

Express error handling works similarly.

## 4. 🔄 Error Handling Flow

Normal request:

```
CLIENT
  |
  v
SERVER
  |
  v
ROUTE
  |
  v
CONTROLLER
  |
  v
SUCCESS RESPONSE
```

Error request:

```
CLIENT
  |
  v
SERVER
  |
  v
ROUTE
  |
  v
CONTROLLER
  |
  v
ERROR OCCURS
  |
  v
ERROR HANDLER
  |
  v
ERROR RESPONSE
  |
  v
CLIENT
```

Important: Express error-handling middleware receives errors passed using `next(error)` or errors forwarded through supported error propagation.

## 5. 🧩 Types of Errors

Let's understand common error categories.

### 1. Syntax Errors

A syntax error happens when JavaScript code does not follow the language syntax.

Incorrect:

```
const name = "Ramesh"
console.log(name
```

There is a missing closing parenthesis.

Correct:

```
const name = "Ramesh";

console.log(name);
```

### 2. Runtime Errors

A runtime error occurs while the program is running.

Example:

```
const student = undefined;

console.log(student.name);
```

This causes an error because `student` is `undefined`.

### 3. Validation Errors

These happen when user input does not satisfy the required rules.

Example:

```
{
    "name": "",
    "course": "Node.js"
}
```

The name is missing.

### 4. Database Errors

These happen when a database operation fails.

Examples:

- Database server is unavailable.
- Invalid database query.
- Connection timeout.

### 5. Not Found Errors

These happen when a requested resource does not exist.

Example:

```
GET /students/100
```

If student 100 does not exist, return `404 Not Found`.

## 6. 💻 Basic Error Handling Example

Let's create a simple API.

```
const express = require("express");

const app = express();

// Normal route
app.get("/", (req, res) => {

    res.send("Welcome to Express");

});

// Error route
app.get("/error", (req, res) => {

    res.status(500).json({
        message: "Something went wrong"
    });

});

// Start server
app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

### Test these URLs

Success:

```
http://localhost:3000/
```

Response:

```
Welcome to Express
```

Error:

```
http://localhost:3000/error
```

Response:

```
{
    "message": "Something went wrong"
}
```

Here, we manually send an error response. In a real application, we should create a reusable error-handling mechanism.

## 7. 🔍 Understanding `try...catch`

`try...catch` is a JavaScript mechanism used to handle exceptions.

It is especially useful when performing operations that may throw errors.

### Syntax

```
try {

    // Code that may cause an error

} catch (error) {

    // Handle the error

}
```

### Basic example

```
try {

    const result = 10 / 0;

    console.log(result);

} catch (error) {

    console.log("Error:", error.message);

}
```

Output:

```
Infinity
```

Why?

JavaScript number division by zero returns `Infinity`. It does not throw an exception.

Let's use an actual error:

```
try {

    const student = undefined;

    console.log(student.name);

} catch (error) {

    console.log("Error:", error.message);

}
```

Output:

```
Error: Cannot read properties of undefined (reading 'name')
```

### Dry run

1. JavaScript enters the `try` block.
2. `student` is assigned `undefined`.
3. Accessing `student.name` throws an error.
4. JavaScript skips the remaining `try` statements.
5. Execution moves to `catch`.
6. The error message is printed.

### `try...catch` in Express controller

```
const getStudents = (req, res) => {

    try {

        const students = [
            { id: 1, name: "Ramesh" },
            { id: 2, name: "Kumar" }
        ];

        res.status(200).json({
            data: students
        });

    } catch (error) {

        res.status(500).json({
            message: error.message
        });

    }

};
```

## 8. ⚡ Understanding `throw new Error()`

`throw new Error()` creates and throws a JavaScript error.

Example:

```
const age = 15;

if (age < 18) {

    throw new Error("You must be at least 18 years old");

}
```

This throws an error when the age is below 18.

### Using `throw` with `try...catch`

```
try {

    const age = 15;

    if (age < 18) {

        throw new Error("You are not eligible");

    }

    console.log("Access granted");

} catch (error) {

    console.log(error.message);

}
```

Output:

```
You are not eligible
```

### Understanding the flow

```
START
  |
  v
Check age
  |
  v
Is age < 18?
  |
  +---- YES
  |       |
  |       v
  |   throw Error
  |       |
  |       v
  |   catch block
  |       |
  |       v
  |   Print error
  |
  +---- NO
          |
          v
     Access granted
```

Remember:

- `throw` creates or raises an error.
- `try` contains code that may fail.
- `catch` handles the error.

## 9. 🔄 Understanding `next(error)`

In Express, we can forward an error to error-handling middleware using:

```
next(error);
```

### Example

```
app.get("/error", (req, res, next) => {

    const error = new Error("Something went wrong");

    next(error);

});
```

What happens?

1. Request reaches `/error`.
2. Express creates an error.
3. `next(error)` forwards it.
4. Express looks for error-handling middleware.
5. The error middleware handles it.

We will create that middleware next.

## 10. 🛠️ Error-handling Middleware

Error-handling middleware is a special Express middleware function that handles errors passed to Express.

It has four parameters:

```
(err, req, res, next) => {

    // Handle error

}
```

### Basic example

```
const express = require("express");

const app = express();

// Normal route
app.get("/error", (req, res, next) => {

    const error = new Error("Student data failed");

    next(error);

});

// Error-handling middleware
app.use((err, req, res, next) => {

    console.error(err.message);

    res.status(500).json({
        message: err.message
    });

});

// Start server
app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Request:

```
GET http://localhost:3000/error
```

Response:

```
{
    "message": "Student data failed"
}
```

Terminal:

```
Student data failed
```

### Important points

- Error middleware has four parameters.
- Its first parameter is `err`.
- Register it after routes.
- Use `next(error)` to forward an error.
- Do not expose sensitive internal details to clients.

## 11. 🏗️ Practical Example — Student CRUD API

Now let's build a practical Student API with centralized error handling.

### Step 1: Project structure

```
student-management/
│
├── server.js
│
├── data/
│   └── students.js
│
├── routes/
│   └── studentRoutes.js
│
├── controllers/
│   └── studentController.js
│
└── middleware/
    └── errorMiddleware.js
```

### Step 2: Create `data/students.js`

```
// Initial student data

let students = [
    {
        id: 1,
        name: "Ramesh",
        course: "Node.js",
        age: 25
    },
    {
        id: 2,
        name: "Kumar",
        course: "React.js",
        age: 24
    },
    {
        id: 3,
        name: "Suresh",
        course: "Python",
        age: 26
    }
];

// Export data
module.exports = students;
```

### Step 3: Create `controllers/studentController.js`

```
// Import student data
const students = require("../data/students");

// ==================================
// GET: All students
// ==================================

const getStudents = (req, res) => {

    res.status(200).json({
        message: "Students fetched successfully",
        data: students
    });

};

// ==================================
// GET: Student by ID
// ==================================

const getStudentById = (req, res, next) => {

    try {

        const id = Number(req.params.id);

        // Validate ID
        if (!Number.isInteger(id) || id <= 0) {

            const error = new Error("Invalid student ID");

            error.statusCode = 400;

            throw error;

        }

        // Find student
        const student = students.find((item) => item.id === id);

        // Check student
        if (!student) {

            const error = new Error("Student not found");

            error.statusCode = 404;

            throw error;

        }

        // Send response
        res.status(200).json({
            message: "Student found",
            data: student
        });

    } catch (error) {

        next(error);

    }

};

// ==================================
// POST: Create student
// ==================================

const createStudent = (req, res, next) => {

    try {

        const { name, course, age } = req.body;

        // Validate required fields
        if (!name || !course || age === undefined) {

            const error = new Error(
                "Name, course and age are required"
            );

            error.statusCode = 400;

            throw error;

        }

        // Validate age
        if (!Number.isInteger(age) || age <= 0) {

            const error = new Error("Age must be a positive integer");

            error.statusCode = 400;

            throw error;

        }

        // Create student
        const newStudent = {

            id: students.length
                ? Math.max(...students.map((item) => item.id)) + 1
                : 1,

            name,
            course,
            age

        };

        // Add student
        students.push(newStudent);

        res.status(201).json({
            message: "Student created successfully",
            data: newStudent
        });

    } catch (error) {

        next(error);

    }

};

// ==================================
// DELETE: Student
// ==================================

const deleteStudent = (req, res, next) => {

    try {

        const id = Number(req.params.id);

        // Validate ID
        if (!Number.isInteger(id) || id <= 0) {

            const error = new Error("Invalid student ID");

            error.statusCode = 400;

            throw error;

        }

        // Find index
        const index = students.findIndex((item) => item.id === id);

        // Check student
        if (index === -1) {

            const error = new Error("Student not found");

            error.statusCode = 404;

            throw error;

        }

        // Delete student
        const deletedStudent = students.splice(index, 1)[0];

        res.status(200).json({
            message: "Student deleted successfully",
            data: deletedStudent
        });

    } catch (error) {

        next(error);

    }

};

// Export controllers
module.exports = {
    getStudents,
    getStudentById,
    createStudent,
    deleteStudent
};
```

### Step 4: Create `routes/studentRoutes.js`

```
// Import Express
const express = require("express");

// Create router
const router = express.Router();

// Import controllers
const {
    getStudents,
    getStudentById,
    createStudent,
    deleteStudent
} = require("../controllers/studentController");

// GET all students
router.get("/", getStudents);

// GET student by ID
router.get("/:id", getStudentById);

// POST new student
router.post("/", createStudent);

// DELETE student
router.delete("/:id", deleteStudent);

// Export router
module.exports = router;
```

### Step 5: Create `middleware/errorMiddleware.js`

```
// Centralized error-handling middleware

const errorMiddleware = (err, req, res, next) => {

    // Get status code or use 500
    const statusCode = err.statusCode || 500;

    // Log error for developer
    console.error(err.message);

    // Send error response
    res.status(statusCode).json({

        success: false,

        message: err.message || "Internal Server Error"

    });

};

// Export middleware
module.exports = errorMiddleware;
```

### Step 6: Create `server.js`

```
// Import Express
const express = require("express");

// Import routes
const studentRoutes = require("./routes/studentRoutes");

// Import error middleware
const errorMiddleware = require("./middleware/errorMiddleware");

// Create Express app
const app = express();

// Port
const PORT = 3000;

// Parse JSON
app.use(express.json());

// Register routes
app.use("/api/students", studentRoutes);

// Error-handling middleware
app.use(errorMiddleware);

// Start server
app.listen(PORT, () => {

    console.log(`Server running on port ${PORT}`);

});
```

### Step 7: Test using Postman

1\. Get all students

```
GET http://localhost:3000/api/students
```

Expected status: `200 OK`

2\. Get student by ID

```
GET http://localhost:3000/api/students/1
```

Expected status: `200 OK`

3\. Get a student that does not exist

```
GET http://localhost:3000/api/students/100
```

Expected status: `404 Not Found`

Response:

```
{
    "success": false,
    "message": "Student not found"
}
```

4\. Get using invalid ID

```
GET http://localhost:3000/api/students/abc
```

Expected status: `400 Bad Request`

Response:

```
{
    "success": false,
    "message": "Invalid student ID"
}
```

5\. Create student with missing data

```
POST http://localhost:3000/api/students
```

Body:

```
{
    "name": "Anil"
}
```

Expected status: `400 Bad Request`

Response:

```
{
    "success": false,
    "message": "Name, course and age are required"
}
```

6\. Create student successfully

Body:

```
{
    "name": "Anil",
    "course": "FastAPI",
    "age": 23
}
```

Expected status: `201 Created`

### Step 8: Understand the error flow

Example request:

```
GET /api/students/100
```

Execution:

```
CLIENT REQUEST
      |
      v
studentRoutes.js
      |
      v
getStudentById()
      |
      v
Find student with ID 100
      |
      v
Student found?
      |
      +---- NO
      |      |
      |      v
      |   Create Error
      |      |
      |      v
      |   throw error
      |      |
      |      v
      |   catch(error)
      |      |
      |      v
      |   next(error)
      |      |
      |      v
      |   errorMiddleware
      |      |
      |      v
      |   404 JSON Response
      |
      +---- YES
             |
             v
        200 JSON Response
```

Important: Our example uses an in-memory array. Later, we will use database operations and handle database errors too.

## 12. 📊 HTTP Status Codes

HTTP status codes tell the client whether a request succeeded or failed.

| Status | Name                  | Meaning                                  |
| ------ | --------------------- | ---------------------------------------- |
| 200    | OK                    | Request successful                       |
| 201    | Created               | New resource created                     |
| 204    | No Content            | Successful request with no response body |
| 400    | Bad Request           | Invalid request data                     |
| 401    | Unauthorized          | Authentication required or failed        |
| 403    | Forbidden             | Access not allowed                       |
| 404    | Not Found             | Resource does not exist                  |
| 409    | Conflict              | Request conflicts with existing data     |
| 500    | Internal Server Error | Unexpected server error                  |
| 503    | Service Unavailable   | Service temporarily unavailable          |

### Simple example

```
res.status(200).json({
    message: "Success"
});
```

```
res.status(404).json({
    message: "Student not found"
});
```

```
res.status(500).json({
    message: "Internal Server Error"
});
```

Remember: Use the status code that best describes the result of the request.

## 13. ⚠️ Common Mistakes

### Mistake 1: Forgetting `next(error)`

Incorrect:

```
catch (error) {

    console.log(error.message);

}
```

The error is not forwarded to Express error middleware.

Correct:

```
catch (error) {

    next(error);

}
```

### Mistake 2: Incorrect error middleware parameters

Incorrect:

```
app.use((req, res, next) => {

    // Error handling

});
```

This is normal middleware, not Express error-handling middleware.

Correct:

```
app.use((err, req, res, next) => {

    // Error handling

});
```

### Mistake 3: Registering error middleware before routes

Incorrect:

```
app.use(errorMiddleware);

app.use("/api/students", studentRoutes);
```

Correct:

```
app.use("/api/students", studentRoutes);

app.use(errorMiddleware);
```

### Mistake 4: Sending multiple responses

Incorrect:

```
if (!student) {

    res.status(404).json({
        message: "Not found"
    });

}

res.json(student);
```

Correct:

```
if (!student) {

    return res.status(404).json({
        message: "Not found"
    });

}
```

### Mistake 5: Exposing internal errors

Avoid sending database credentials, connection strings, stack traces, or other sensitive details to the client.

## 14. ⭐ Best Practices

1. Use centralized error-handling middleware.
2. Use meaningful error messages.
3. Use correct HTTP status codes.
4. Validate user input.
5. Use `try...catch` when needed.
6. Forward errors with `next(error)`.
7. Register error middleware after routes.
8. Log useful error details on the server.
9. Do not expose sensitive information to clients.
10. Keep error responses consistent.

### A good API error response format

```
{
    "success": false,
    "message": "Student not found"
}
```

For larger projects, you can also include a stable error code:

```
{
    "success": false,
    "message": "Student not found",
    "errorCode": "STUDENT_NOT_FOUND"
}
```

## 15. 🎯 Interview Questions

## 16. 📝 Practice Problems

Try these exercises.

- Problem 1: Create an API that returns `404` when a student is not found.
- Problem 2: Use `try...catch` in a controller.
- Problem 3: Create a custom error using `throw new Error()`.
- Problem 4: Forward errors using `next(error)`.
- Problem 5: Create centralized error-handling middleware.
- Problem 6: Return `400` when required request body fields are missing.
- Problem 7: Create a consistent JSON error response format.

## 17. 🏆 Mini Challenge — Employee API Error Handling

### Requirement

Add error handling to your Employee Management API.

### Initial raw data

```
let employees = [
    {
        id: 1,
        name: "Ramesh",
        department: "IT",
        salary: 30000
    },
    {
        id: 2,
        name: "Kumar",
        department: "HR",
        salary: 25000
    },
    {
        id: 3,
        name: "Suresh",
        department: "Finance",
        salary: 35000
    }
];
```

### Your tasks

1. Create `errorMiddleware.js`.
2. Create a `getEmployeeById` controller.
3. Validate the employee ID.
4. Return `400` for an invalid ID.
5. Return `404` when an employee does not exist.
6. Use `next(error)` to forward errors.
7. Register error middleware in `server.js`.

### Expected results

| Request              | Expected status |
| -------------------- | --------------- |
| `/api/employees/1`   | 200             |
| `/api/employees/100` | 404             |
| `/api/employees/abc` | 400             |

### Logic-building steps

Step 1 — Requirement: Handle invalid and missing employee IDs.

Step 2 — Input: Employee ID from URL.

Step 3 — Output: Employee data or error response.

Step 4 — Break into steps:

```
Read Employee ID
       |
       v
Validate ID
       |
       v
Find Employee
       |
       v
Employee Exists?
       |
       +---- YES ---> Return 200
       |
       +---- NO ----> Return 404
```

Step 5 — Hint:

```
const id = Number(req.params.id);
```

Step 6 — Pseudocode:

```
START

Read employee ID

IF ID is invalid
    Create 400 error
    Forward error
ELSE
    Find employee

    IF employee not found
        Create 404 error
        Forward error
    ELSE
        Return employee
    END IF

END IF

END
```

Step 7 — Your turn!

Try writing the controller and error middleware. Send your code, and I will explain and correct it line by line.

## 18. 📌 Chapter Summary & Quick Revision

### What did we learn?

| Concept          | Meaning                               |
| ---------------- | ------------------------------------- |
| Error Handling   | Managing application errors           |
| `try`            | Contains code that may throw an error |
| `catch`          | Handles exceptions                    |
| `throw`          | Raises an error                       |
| `new Error()`    | Creates an Error object               |
| `next(error)`    | Forwards error to Express             |
| Error Middleware | Handles forwarded errors              |
| `400`            | Bad Request                           |
| `401`            | Unauthorized                          |
| `404`            | Not Found                             |
| `500`            | Internal Server Error                 |

### Final request flow

```
CLIENT
  |
  v
ROUTES
  |
  v
CONTROLLER
  |
  v
ERROR OCCURS?
  |
  +---- NO ----> SUCCESS RESPONSE
  |
  +---- YES ---> next(error)
                    |
                    v
              ERROR MIDDLEWARE
                    |
                    v
               ERROR RESPONSE
```

### Self-check

- I understand error handling.
- I can use `try...catch`.
- I understand `throw new Error()`.
- I understand `next(error)`.
- I can create error-handling middleware.
- I know common HTTP status codes.
- I can handle errors in a CRUD API.

## 🎓 Next Chapter

PART 6 — REST API DEVELOPMENT

Chapter 23 — Introduction to REST API

We will learn:

- What is an API?
- What is REST?
- What is REST API?
- REST API vs Normal API
- Client-server architecture
- HTTP methods
- HTTP status codes
- JSON request and response
- REST principles
- Resource-based URLs
- Practical Student REST API

Type `NEXT` to start Chapter 23.