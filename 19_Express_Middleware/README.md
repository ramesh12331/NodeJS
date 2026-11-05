# 🚀 PART 5 — EXPRESS.JS

# Chapter 19 — Express Middleware

BEGINNER LEVEL → PRACTICAL LEVEL

## 📚 Table of Contents

1. What is Middleware?
2. Why do we need Middleware?
3. Real-world Analogy
4. Middleware Request Flow
5. Middleware Syntax
6. Basic Middleware Example
7. Middleware Dry Run
8. Middleware Output
9. Line-by-Line Explanation
10. Practical Example — Student API
11. Types of Middleware
12. Common Mistakes
13. Best Practices
14. Interview Questions
15. Practice Problems
16. Mini Challenge
17. Chapter Summary & Quick Revision

## 1. 🧠 What is Middleware?

Middleware is a function that runs between the incoming request and the final response.

In simple words:

When a client sends a request to the Express server, middleware gets a chance to process that request before the route sends a response.

### Middleware function

```
(req, res, next) => {
    // Middleware logic
}
```

There are three important parameters:

| Parameter | Meaning                                                |
| --------- | ------------------------------------------------------ |
| `req`     | Contains request information                           |
| `res`     | Used to send a response                                |
| `next`    | Passes control to the next middleware or route handler |

### Simple example

```
function myMiddleware(req, res, next) {
    console.log("Middleware is running");

    next();
}
```

Important: `next()` tells Express to continue to the next middleware or route handler.

## 2. 🤔 Why do we need Middleware?

Imagine you are developing a Student Management API.

You have these routes:

```
GET     /students
GET     /students/1
POST    /students
PUT     /students/1
DELETE  /students/1
```

Before processing these requests, you may need to:

- Check whether the user is logged in.
- Check the request body.
- Display request information in the terminal.
- Check whether the user has permission.
- Handle errors.

Without middleware, you might repeat the same code inside every route.

Middleware helps us write reusable code.

## 3. 🌍 Real-world Analogy

Imagine entering an office building.

```
You arrive at the office
        |
        v
Security checks your ID
        |
        v
Reception checks your details
        |
        v
Manager gives permission
        |
        v
You enter the office
```

Express middleware works similarly:

```
Client Request
      |
      v
Logger Middleware
      |
      v
Authentication Middleware
      |
      v
Validation Middleware
      |
      v
Route Handler
      |
      v
Response to Client
```

Each middleware performs a particular task.

## 4. 🔄 Middleware Request Flow

Let's understand the request flow with an example.

```
Client
  |
  | GET /students
  v
Express Server
  |
  v
Middleware 1: Logger
  |
  | next()
  v
Middleware 2: Authentication
  |
  | next()
  v
Route Handler: GET /students
  |
  v
Send JSON Response
  |
  v
Client
```

### What happens?

1. Client sends a request.
2. Logger middleware prints request information.
3. Authentication middleware checks access.
4. If allowed, it calls `next()`.
5. Express executes the route handler.
6. Server sends a response.

If authentication fails, middleware can send an error response directly without calling `next()`.

## 5. 📝 Middleware Syntax

```
function middlewareName(req, res, next) {

    // Perform some operation

    next();
}
```

Register middleware using `app.use()`:

```
app.use(middlewareName);
```

### Important methods

| Method         | Purpose                                 |
| -------------- | --------------------------------------- |
| `app.use()`    | Registers middleware                    |
| `next()`       | Moves to the next middleware or handler |
| `req.method`   | Gets HTTP method                        |
| `req.url`      | Gets requested URL                      |
| `req.headers`  | Gets request headers                    |
| `res.status()` | Sets HTTP status                        |
| `res.json()`   | Sends JSON response                     |

## 6. 💻 Basic Middleware Example

Let's create our first Express middleware.

### Project structure

```
middleware-demo/
│
├── server.js
└── package.json
```

### Step 1: Install Express

```
npm init -y
npm install express
```

### Step 2: Create `server.js`

```
// Import Express
const express = require("express");

// Create Express application
const app = express();

// Create middleware
function myMiddleware(req, res, next) {

    console.log("Middleware is running");

    // Move to the next handler
    next();
}

// Register middleware
app.use(myMiddleware);

// Create route
app.get("/", (req, res) => {

    res.send("Welcome to Express Middleware");

});

// Start server
app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

### Step 3: Run the server

```
node server.js
```

Open this URL:

```
http://localhost:3000/
```

## 7. 🔍 Middleware Dry Run

Let's understand what happens when we send a request.

### Request

```
GET http://localhost:3000/
```

### Execution steps

Step 1: Express receives the request.

Step 2: Express checks registered middleware.

```
app.use(myMiddleware);
```

Step 3: Middleware executes.

```
console.log("Middleware is running");
```

Terminal output:

```
Middleware is running
```

Step 4: Middleware calls:

```
next();
```

Step 5: Express executes the route:

```
app.get("/", (req, res) => {
    res.send("Welcome to Express Middleware");
});
```

Step 6: Server sends the response.

## 8. 📤 Output

Expected output

Browser response:

```
Welcome to Express Middleware
```

VS Code terminal:

```
Server running on port 3000
Middleware is running
```

Every time you refresh the browser, the middleware runs again.

## 9. 🔎 Line-by-Line Explanation

```
function myMiddleware(req, res, next) {
```

Creates a middleware function.

- `req`: Request data.
- `res`: Response object.
- `next`: Function to continue execution.

```
console.log("Middleware is running");
```

Prints a message in the terminal.

```
next();
```

Passes control to the next middleware or route handler.

```
app.use(myMiddleware);
```

Registers middleware for incoming requests that match its mounting path. Here, it is registered globally.

Remember: If middleware neither sends a response nor calls `next()`, the request may remain pending.

## 10. 🏗️ Practical Example — Student API

Now let's create a practical middleware example using real data.

### Step 1: Create student data

```
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
```

### Step 2: Complete code — `server.js`

```
const express = require("express");

const app = express();

const PORT = 3000;

// Read JSON request body
app.use(express.json());

// ==================================
// MIDDLEWARE 1: LOGGER
// ==================================

function logger(req, res, next) {

    console.log("Request Method:", req.method);

    console.log("Request URL:", req.url);

    console.log("Request Time:", new Date().toLocaleString());

    next();
}

// Register logger middleware
app.use(logger);

// ==================================
// RAW STUDENT DATA
// ==================================

let students = [
    { id: 1, name: "Ramesh", course: "Node.js", age: 25 },
    { id: 2, name: "Kumar", course: "React.js", age: 24 },
    { id: 3, name: "Suresh", course: "Python", age: 26 }
];

// ==================================
// ROUTES
// ==================================

// GET: All students
app.get("/students", (req, res) => {

    res.status(200).json({
        message: "Students fetched successfully",
        data: students
    });

});

// GET: Student by ID
app.get("/students/:id", (req, res) => {

    const id = Number(req.params.id);

    const student = students.find((item) => item.id === id);

    if (!student) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    res.status(200).json({
        message: "Student found",
        data: student
    });

});

// POST: Create student
app.post("/students", (req, res) => {

    const { name, course, age } = req.body;

    if (!name || !course || age === undefined) {

        return res.status(400).json({
            message: "Name, course and age are required"
        });

    }

    const newStudent = {
        id: students.length
            ? Math.max(...students.map((item) => item.id)) + 1
            : 1,
        name,
        course,
        age
    };

    students.push(newStudent);

    res.status(201).json({
        message: "Student created successfully",
        data: newStudent
    });

});

// DELETE: Student
app.delete("/students/:id", (req, res) => {

    const id = Number(req.params.id);

    const index = students.findIndex((item) => item.id === id);

    if (index === -1) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    const deletedStudent = students.splice(index, 1)[0];

    res.status(200).json({
        message: "Student deleted successfully",
        data: deletedStudent
    });

});

// Start server
app.listen(PORT, () => {

    console.log(`Server running on port ${PORT}`);

});
```

### Step 3: Test using Postman

GET all students

```
GET http://localhost:3000/students
```

Expected data:

```
{
    "message": "Students fetched successfully",
    "data": [
        {
            "id": 1,
            "name": "Ramesh",
            "course": "Node.js",
            "age": 25
        },
        {
            "id": 2,
            "name": "Kumar",
            "course": "React.js",
            "age": 24
        },
        {
            "id": 3,
            "name": "Suresh",
            "course": "Python",
            "age": 26
        }
    ]
}
```

POST — Add a student

```
POST http://localhost:3000/students
```

Body → raw → JSON:

```
{
    "name": "Anil",
    "course": "FastAPI",
    "age": 23
}
```

After inserting, the raw data becomes:

```
[
    { id: 1, name: "Ramesh", course: "Node.js", age: 25 },
    { id: 2, name: "Kumar", course: "React.js", age: 24 },
    { id: 3, name: "Suresh", course: "Python", age: 26 },
    { id: 4, name: "Anil", course: "FastAPI", age: 23 }
]
```

### What does the middleware print?

When you send:

```
GET /students
```

Terminal:

```
Request Method: GET
Request URL: /students
Request Time: 11/6/2026, 10:30:00 PM
```

The exact time depends on when you send the request.

Important: Logger middleware runs before the route handler because we registered it before the routes.

## 11. 🧩 Types of Middleware

Express middleware can be grouped into different types.

### 1. Application-level Middleware

Middleware registered using `app.use()` or an application method.

```
function logger(req, res, next) {

    console.log("Request received");

    next();

}

app.use(logger);
```

This middleware runs for requests that match its registered path.

### 2. Router-level Middleware

Middleware registered with an Express Router.

```
const express = require("express");

const router = express.Router();

function checkUser(req, res, next) {

    console.log("Router middleware");

    next();

}

router.use(checkUser);

router.get("/students", (req, res) => {

    res.send("Student list");

});

app.use("/api", router);
```

URL:

```
http://localhost:3000/api/students
```

We will study `express.Router()` in Chapter 20.

### 3. Built-in Middleware

Express provides some middleware functions directly.

| Middleware             | Purpose                     |
| ---------------------- | --------------------------- |
| `express.json()`       | Reads JSON request body     |
| `express.urlencoded()` | Reads URL-encoded form data |
| `express.static()`     | Serves static files         |

Example:

```
app.use(express.json());

app.use(express.urlencoded({ extended: true }));

app.use(express.static("public"));
```

Static files example:

```
project/
│
├── server.js
└── public/
    ├── style.css
    └── logo.png
```

With `express.static("public")`, these files can be accessed through URLs such as:

```
http://localhost:3000/logo.png
```

### 4. Third-party Middleware

Third-party middleware is created by other developers and installed using npm.

Example: Morgan.

Install:

```
npm install morgan
```

Use:

```
const morgan = require("morgan");

app.use(morgan("dev"));
```

Morgan automatically logs request details in the terminal.

Another example is CORS.

Install:

```
npm install cors
```

Use:

```
const cors = require("cors");

app.use(cors());
```

CORS helps control which browser origins can access your API.

### 5. Custom Middleware

Custom middleware is middleware that we create ourselves.

Example:

```
function checkAge(req, res, next) {

    const age = Number(req.query.age);

    if (age < 18 || Number.isNaN(age)) {

        return res.status(403).json({
            message: "You must be at least 18 years old"
        });

    }

    next();

}

app.get("/adult", checkAge, (req, res) => {

    res.send("Access granted");

});
```

Test:

```
GET http://localhost:3000/adult?age=25
```

Response:

```
Access granted
```

Try:

```
GET http://localhost:3000/adult?age=15
```

Response:

```
{
    "message": "You must be at least 18 years old"
}
```

### 6. Error-handling Middleware

Error middleware has four parameters:

```
(err, req, res, next) => {

    // Handle error

}
```

Example:

```
app.get("/error", (req, res, next) => {

    const error = new Error("Something went wrong");

    next(error);

});

// Error-handling middleware
app.use((err, req, res, next) => {

    console.error(err.message);

    res.status(500).json({
        message: err.message
    });

});
```

Response:

```
{
    "message": "Something went wrong"
}
```

Important: Error-handling middleware should be registered after the routes that may pass errors to it.

## 12. ⚠️ Common Mistakes

### Mistake 1: Forgetting `next()`

Incorrect:

```
function logger(req, res, next) {

    console.log("Request received");

}
```

Why incorrect?

The request may remain pending because middleware neither sends a response nor passes control.

Correct:

```
function logger(req, res, next) {

    console.log("Request received");

    next();

}
```

### Mistake 2: Calling `next()` after sending a response

Incorrect:

```
function checkUser(req, res, next) {

    res.send("Access denied");

    next();

}
```

Why incorrect?

You have already sent a response. Continuing can cause errors such as attempting to send headers twice.

Correct:

```
function checkUser(req, res, next) {

    return res.status(403).send("Access denied");

}
```

### Mistake 3: Wrong middleware order

Incorrect:

```
app.post("/students", (req, res) => {

    console.log(req.body);

    res.json(req.body);

});

app.use(express.json());
```

The JSON parser is registered after the route.

Correct:

```
app.use(express.json());

app.post("/students", (req, res) => {

    console.log(req.body);

    res.json(req.body);

});
```

### Mistake 4: Forgetting `return`

Incorrect:

```
if (!student) {

    res.status(404).json({
        message: "Student not found"
    });

}

res.json(student);
```

Correct:

```
if (!student) {

    return res.status(404).json({
        message: "Student not found"
    });

}

res.json(student);
```

## 13. ⭐ Best Practices

- Register middleware in the correct order.
- Keep each middleware responsible for one task.
- Use meaningful names like `logger`, `authenticateUser`, and `validateStudent`.
- Use `return` after sending an early error response.
- Never expose sensitive information in error messages.
- Use environment variables for secrets.
- Use appropriate HTTP status codes.
- Keep reusable middleware in a separate folder as your project grows.

### Recommended project structure

```
student-api/
│
├── middleware/
│   ├── logger.js
│   ├── authMiddleware.js
│   └── errorMiddleware.js
│
├── routes/
│   └── studentRoutes.js
│
├── controllers/
│
├── server.js
└── package.json
```

### Example: Separate Logger Middleware

`middleware/logger.js`

```
function logger(req, res, next) {

    console.log(`${req.method} ${req.url}`);

    next();

}

module.exports = logger;
```

`server.js`

```
const express = require("express");

const logger = require("./middleware/logger");

const app = express();

app.use(express.json());

app.use(logger);

app.get("/", (req, res) => {

    res.send("Home Page");

});

app.listen(3000);
```

## 14. 🎯 Interview Questions

## 15. 📝 Practice Problems

Try these exercises yourself.

- Problem 1: Create middleware that prints `"Welcome to my API"` for every request.
- Problem 2: Create middleware that displays the HTTP method and URL.
- Problem 3: Create middleware that checks the user's age.
- Problem 4: Create middleware that checks whether a username exists in `req.body`.
- Problem 5: Create middleware that blocks access when a request does not contain an expected API key.
- Problem 6: Create an error-handling middleware that returns status code `500`.

## 16. 🏆 Mini Challenge — Student API Authentication

Requirement: Create a middleware that protects your Student API.

### Step 1: Requirement

Only users with a valid API key can access:

```
GET /students
```

### Step 2: Input

Expected request header:

```
x-api-key: my-secret-key
```

### Step 3: Output

If the key is correct:

```
{
    "message": "Access granted"
}
```

If the key is missing or incorrect:

```
{
    "message": "Unauthorized access"
}
```

### Step 4: Break into steps

1. Create an authentication middleware.
2. Read the API key from `req.headers`.
3. Compare it with the expected key.
4. If correct, call `next()`.
5. Otherwise, return status `401`.

### Step 5: Hint

Read the request header using:

```
req.headers["x-api-key"]
```

### Step 6: Pseudocode

```
START

Read API key from request header

IF API key is correct
    Call next()
ELSE
    Send 401 Unauthorized response

END
```

### Step 7: Your turn

Write the middleware and register it only for the `/students` route.

Do not worry if your code has mistakes. Send your attempt, and I'll review it line by line.

## 17. 📌 Chapter Summary & Quick Revision

### What did we learn?

| Concept          | Meaning                                          |
| ---------------- | ------------------------------------------------ |
| Middleware       | Function that runs during request-response cycle |
| `req`            | Request information                              |
| `res`            | Response object                                  |
| `next()`         | Passes control forward                           |
| `app.use()`      | Registers application middleware                 |
| `router.use()`   | Registers router middleware                      |
| `express.json()` | Parses JSON request body                         |
| Morgan           | Third-party logger                               |
| CORS             | Controls cross-origin browser access             |
| Error middleware | Handles errors                                   |

### Final revision flow

```
CLIENT REQUEST
      |
      v
EXPRESS SERVER
      |
      v
MIDDLEWARE
      |
      +----> Check Request
      |
      +----> Authentication
      |
      +----> Validation
      |
      v
ROUTE HANDLER
      |
      v
RESPONSE
```

### Self-check

- I understand what middleware is.
- I understand `req`, `res`, and `next`.
- I can create custom middleware.
- I understand middleware order.
- I can use built-in middleware.
- I understand error-handling middleware.
- I can protect an API using middleware.

## 🎓 Next Chapter

Chapter 20 — Express Router

We will learn:

- What is Express Router?
- Why do we need Router?
- `express.Router()`
- Creating separate route files
- `router.get()`, `router.post()`, `router.put()`, `router.delete()`
- Connecting routes with `server.js`
- Practical Student API using separate route files
- Complete folder structure

Type `NEXT` to start Chapter 20.