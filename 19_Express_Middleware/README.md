# 🚀 PART 5 — EXPRESS.JS

# Chapter 19 — Express Middleware

Beginner to Advanced • GitHub README Notes • Node.js + Express.js

In this chapter, you will learn how Express middleware works, how a request travels through middleware, and how to build Logger, Authentication, and Validation middleware.

## 📚 Table of Contents

1. What is Middleware?
2. Why Do We Need Middleware?
3. Real-World Analogy
4. Request Lifecycle
5. Middleware Syntax
6. Basic Middleware Example
7. Dry Run
8. Output
9. Line-by-Line Explanation
10. Types of Middleware
11. Common Mistakes
12. Best Practices
13. Interview Questions
14. Practice Problems
15. Mini Challenge
16. Chapter Summary
17. Quick Revision

## 1. 🧠 What is Middleware?

Definition: Middleware is a function that executes during the request-response cycle of an Express application.

Middleware can:

- Execute some code.
- Read or modify the request (`req`).
- Read or modify the response (`res`).
- End the request-response cycle.
- Pass control to the next middleware using `next()`.

Simple example: Before allowing a user to access a protected API, middleware can check whether the user is authenticated.

### Basic middleware structure

```
function myMiddleware(req, res, next) {
    console.log("Middleware executed");

    next();
}
```

Important words:

| Keyword | Meaning                                          |
| ------- | ------------------------------------------------ |
| `req`   | Contains client request information              |
| `res`   | Used to send a response to the client            |
| `next`  | Passes control to the next middleware or handler |

## 2. ❓ Why Do We Need Middleware?

Imagine you are building a Book Management API.

You have many routes:

```
GET     /books
POST    /books
GET     /books/1
PUT     /books/1
DELETE  /books/1
```

You may need to perform the same tasks for multiple routes:

- Check whether the user is logged in.
- Check whether the request contains valid data.
- Record the request details.
- Handle errors.
- Parse JSON request data.

Without middleware, you might repeat the same code inside every route.

Middleware helps us reuse common logic instead of writing the same code repeatedly.

### Without middleware

```
app.get("/books", (req, res) => {
    console.log("Request received");
    res.send("Books");
});

app.get("/students", (req, res) => {
    console.log("Request received");
    res.send("Students");
});

app.get("/courses", (req, res) => {
    console.log("Request received");
    res.send("Courses");
});
```

Here, we repeat the logging code.

### With middleware

```
function logger(req, res, next) {
    console.log("Request received");

    next();
}

app.use(logger);

app.get("/books", (req, res) => {
    res.send("Books");
});

app.get("/students", (req, res) => {
    res.send("Students");
});

app.get("/courses", (req, res) => {
    res.send("Courses");
});
```

Now one middleware function can handle logging for all these routes.

## 3. 🏢 Real-World Analogy

Imagine you are entering an office building.

[Visitor Management System for Offices and Modern Workplaces](https://images.openai.com/static-rsc-4/3tKF4fqKyJp020_IM6i25qiMqRHnZQJiTShuCaUoYM2SSeJGSK_-PyupVzb7FODsNf6hPk3LJcLSqHNfwV-rd1FiggUEsaOz13389Xezd64sjnezLeBD8KMctpw4vdoREaU6_-HbPUYoel1EPSoUimE4lyzC9X0JF2A_ajGbmNQ?purpose=inline)

[digitalreception.app](https://digitalreception.app/blog/visitor-management-system-for-offices-and-modern-workplaces?utm_source=chatgpt.com)

Before entering the office:

1. Security checks your identity.
2. Reception verifies your appointment.
3. You receive permission to enter.
4. You reach your destination.

Express middleware works in a similar way.

| Office building          | Express.js                |
| ------------------------ | ------------------------- |
| Visitor                  | Client                    |
| Security check           | Authentication middleware |
| Appointment verification | Validation middleware     |
| Entry permission         | `next()`                  |
| Office room              | Route handler             |
| Entry denied             | Error response            |

Middleware acts like a checkpoint between the client and the route handler.

## 4. 🔄 Request Lifecycle

When a client sends an HTTP request, Express processes it through middleware and eventually sends a response.

### Visual flowchart

```
          CLIENT
            |
            | HTTP REQUEST
            v
      EXPRESS SERVER
            |
            v
    +------------------+
    |  Logger          |
    |  Middleware      |
    +------------------+
            |
            v
    +------------------+
    |  Authentication  |
    |  Middleware      |
    +------------------+
            |
            v
    +------------------+
    |  Validation      |
    |  Middleware      |
    +------------------+
            |
            v
    +------------------+
    |  ROUTE HANDLER   |
    +------------------+
            |
            v
       HTTP RESPONSE
            |
            v
          CLIENT
```

Important: Middleware executes in the order in which it is registered.

### What happens if authentication fails?

```
       CLIENT REQUEST
             |
             v
     AUTHENTICATION
       MIDDLEWARE
             |
             v
       Is user valid?
          /     \
        YES      NO
         |        |
         v        v
      next()   401 ERROR
         |        |
         v        v
    ROUTE       CLIENT
    HANDLER
```

If middleware sends a response, it does not need to call `next()`.

## 5. 📝 Middleware Syntax

### General syntax

```
app.use((req, res, next) => {

    // Middleware logic

    next();

});
```

### Explanation

- `app.use()` — Registers middleware.
- `req` — Request object.
- `res` — Response object.
- `next()` — Moves control forward.

### Named middleware

```
function checkRequest(req, res, next) {

    console.log("Checking request");

    next();
}

app.use(checkRequest);
```

You can create middleware separately and register it using `app.use()`.

## 6. 💻 Basic Middleware Example

### Step 1: Create project

```
mkdir middleware-demo

cd middleware-demo

npm init -y

npm install express
```

### Step 2: Create `server.js`

```
const express = require("express");

const app = express();

const PORT = 3000;

// =================================
// CUSTOM MIDDLEWARE
// =================================

function myMiddleware(req, res, next) {

    console.log("Middleware executed");

    next();
}

// Register middleware
app.use(myMiddleware);

// =================================
// ROUTES
// =================================

app.get("/", (req, res) => {

    res.send("Welcome to Express");

});

app.get("/books", (req, res) => {

    res.send("Book List");

});

// =================================
// START SERVER
// =================================

app.listen(PORT, () => {

    console.log(`Server running on port ${PORT}`);

});
```

### Step 3: Run the server

```
node server.js
```

### Step 4: Test in browser

```
http://localhost:3000/
```

```
http://localhost:3000/books
```

## 7. 🔍 Dry Run

Let's understand what happens when you visit:

```
http://localhost:3000/books
```

| Step | Execution                 | Result           |
| ---- | ------------------------- | ---------------- |
| 1    | Client sends GET request  | `/books`         |
| 2    | Express receives request  | Request received |
| 3    | `myMiddleware()` executes | Logs message     |
| 4    | `next()` executes         | Passes control   |
| 5    | `/books` route matches    | Route executes   |
| 6    | `res.send()` executes     | Sends response   |

Remember: `next()` tells Express to continue processing the request.

## 8. 📤 Output

### Browser output

```
Book List
```

### Terminal output

```
Server running on port 3000

Middleware executed
Middleware executed
```

You will see the middleware message whenever you make a request to a route registered after this application-level middleware.

## 9. 🔬 Line-by-Line Explanation

```
function myMiddleware(req, res, next) {
```

Creates a middleware function.

```
console.log("Middleware executed");
```

Prints a message in the terminal.

```
next();
```

Passes control to the next middleware or matching route handler.

```
app.use(myMiddleware);
```

Registers the middleware with the Express application.

```
app.get("/books", (req, res) => {
    res.send("Book List");
});
```

Creates a GET route that sends the response.

### Test your understanding

## 10. 🧩 Types of Middleware

Express middleware can be divided into several types.

### 10.1 Application-Level Middleware

Definition: Application-level middleware is middleware registered on an Express application using `app.use()` or an HTTP method such as `app.get()`.

Example:

```
const express = require("express");

const app = express();

// Application-level middleware
app.use((req, res, next) => {

    console.log("Application middleware");

    next();

});

app.get("/", (req, res) => {

    res.send("Home Page");

});

app.listen(3000);
```

This middleware runs for requests that pass through its registration point and match its mounted path.

### 10.2 Router-Level Middleware

Definition: Router-level middleware is middleware attached to an Express Router instance.

It is useful when you have multiple routes related to one module.

Example:

```
const express = require("express");

const app = express();

const router = express.Router();

// Router-level middleware
router.use((req, res, next) => {

    console.log("Book router middleware");

    next();

});

// Book routes
router.get("/", (req, res) => {

    res.send("All Books");

});

router.get("/:id", (req, res) => {

    res.send("Single Book");

});

// Register router
app.use("/books", router);

app.listen(3000);
```

Test:

```
GET http://localhost:3000/books
GET http://localhost:3000/books/1
```

Router middleware applies to requests handled by that router after the middleware is registered.

### 10.3 Built-in Middleware

Definition: Built-in middleware is middleware provided by Express itself.

Important built-in middleware:

| Middleware             | Purpose                             |
| ---------------------- | ----------------------------------- |
| `express.json()`       | Parses incoming JSON request bodies |
| `express.urlencoded()` | Parses URL-encoded request bodies   |
| `express.static()`     | Serves static files                 |

#### Example 1: express.json()

```
const express = require("express");

const app = express();

// Parse incoming JSON data
app.use(express.json());

app.post("/students", (req, res) => {

    console.log(req.body);

    res.json({
        message: "Student received",
        data: req.body
    });

});

app.listen(3000);
```

Postman request:

```
POST http://localhost:3000/students
```

Body → raw → JSON:

```
{
    "name": "Ramesh",
    "age": 25,
    "course": "Node.js"
}
```

Expected response:

```
{
    "message": "Student received",
    "data": {
        "name": "Ramesh",
        "age": 25,
        "course": "Node.js"
    }
}
```

Without `express.json()`, Express does not automatically parse incoming JSON request bodies.

#### Example 2: express.urlencoded()

```
app.use(express.urlencoded({ extended: true }));
```

This middleware parses form data sent using URL-encoded encoding.

#### Example 3: express.static()

```
app.use(express.static("public"));
```

Suppose your project contains:

```
project/
│
├── server.js
│
└── public/
    ├── index.html
    └── style.css
```

You can access the file:

```
http://localhost:3000/index.html
```

### 10.4 Third-Party Middleware

Definition: Third-party middleware is middleware developed by external developers or packages and installed into your project.

Examples:

| Package  | Purpose                            |
| -------- | ---------------------------------- |
| `cors`   | Controls cross-origin access       |
| `morgan` | HTTP request logging               |
| `helmet` | Adds security-related HTTP headers |

Install:

```
npm install cors morgan helmet
```

Example:

```
const express = require("express");

const cors = require("cors");

const morgan = require("morgan");

const helmet = require("helmet");

const app = express();

// Enable CORS
app.use(cors());

// Log HTTP requests
app.use(morgan("dev"));

// Add security headers
app.use(helmet());

app.get("/", (req, res) => {

    res.send("Middleware Example");

});

app.listen(3000);
```

Third-party middleware saves development time because you can reuse tested functionality.

### 10.5 Custom Middleware

Definition: Custom middleware is middleware that you create yourself to perform application-specific tasks.

Example:

```
function welcomeMiddleware(req, res, next) {

    req.message = "Welcome to Node.js";

    next();

}

app.use(welcomeMiddleware);

app.get("/", (req, res) => {

    res.send(req.message);

});
```

Output:

```
Welcome to Node.js
```

Notice that we added a new property to `req`:

```
req.message = "Welcome to Node.js";
```

The next handler can access it.

### 10.6 Error-Handling Middleware

Definition: Error-handling middleware is middleware designed to handle errors that occur during request processing.

Important: Error-handling middleware has four parameters: `err`, `req`, `res`, and `next`.

Syntax:

```
function errorHandler(err, req, res, next) {

    res.status(500).json({
        message: "Something went wrong"
    });

}
```

Complete example:

```
const express = require("express");

const app = express();

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

app.listen(3000);
```

Test:

```
GET http://localhost:3000/error
```

Output:

```
{
    "message": "Something went wrong"
}
```

Calling `next(error)` passes the error to Express error-handling middleware.

### 10.7 Logger Middleware — Practical Example

Requirement: Whenever a client sends a request, display its HTTP method and URL in the terminal.

```
function loggerMiddleware(req, res, next) {

    console.log("Method:", req.method);

    console.log("URL:", req.url);

    console.log("Time:", new Date().toLocaleString());

    next();

}

app.use(loggerMiddleware);
```

Example terminal output:

```
Method: GET
URL: /books
Time: 11/6/2026, 10:30:00 PM
```

Use logger middleware to monitor incoming HTTP requests during development.

### 10.8 Authentication Middleware

Requirement: Allow access to a protected API only when the client provides the correct API token.

```
function authMiddleware(req, res, next) {

    const token = req.headers.authorization;

    // Check whether token exists
    if (!token) {

        return res.status(401).json({
            message: "Authorization token required"
        });

    }

    // Example: compare with an environment variable
    if (token !== `Bearer ${process.env.API_TOKEN}`) {

        return res.status(403).json({
            message: "Invalid token"
        });

    }

    // Token is valid
    next();

}
```

Register it for a protected route:

```
app.get("/profile", authMiddleware, (req, res) => {

    res.json({
        message: "Welcome to your profile"
    });

});
```

For this example, configure `API_TOKEN` in your environment. You can use the `dotenv` package to load a local `.env` file during development.

Important status codes:

| Status | Meaning                              |
| ------ | ------------------------------------ |
| `401`  | Authentication is missing or invalid |
| `403`  | Access is forbidden                  |

This is a learning example. Real applications should use a properly designed authentication system, such as verified JWTs or sessions, and protect secrets.

### 10.9 Validation Middleware

Requirement: Before creating a student, check whether the name and email are provided.

```
function validateStudent(req, res, next) {

    const { name, email } = req.body;

    // Check name
    if (!name) {

        return res.status(400).json({
            message: "Name is required"
        });

    }

    // Check email
    if (!email) {

        return res.status(400).json({
            message: "Email is required"
        });

    }

    next();

}
```

Use it in a POST route:

```
app.use(express.json());

app.post("/students", validateStudent, (req, res) => {

    res.status(201).json({
        message: "Student created successfully",
        student: req.body
    });

});
```

Valid request:

```
{
    "name": "Ramesh",
    "email": "ramesh@example.com"
}
```

Response:

```
{
    "message": "Student created successfully",
    "student": {
        "name": "Ramesh",
        "email": "ramesh@example.com"
    }
}
```

Invalid request:

```
{
    "name": "Ramesh"
}
```

Response:

```
{
    "message": "Email is required"
}
```

Validation middleware checks incoming data before the route performs its main operation.

## 11. ⚠️ Common Mistakes

### Mistake 1: Forgetting next()

Incorrect:

```
app.use((req, res, next) => {

    console.log("Middleware");

});
```

Problem: The request may remain pending because control is not passed forward and no response is sent.

Correct:

```
app.use((req, res, next) => {

    console.log("Middleware");

    next();

});
```

### Mistake 2: Calling next() after sending a response

Incorrect:

```
app.use((req, res, next) => {

    res.send("Hello");

    next();

});
```

Problem: You are trying to continue processing after sending the response. This can cause errors.

Correct:

```
app.use((req, res, next) => {

    return res.send("Hello");

});
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

Correct:

```
app.use(express.json());

app.post("/students", (req, res) => {

    console.log(req.body);

    res.json(req.body);

});
```

Register body-parsing middleware before routes that need the parsed request body.

### Mistake 4: Wrong error middleware parameters

Incorrect:

```
app.use((req, res, next) => {

    console.log("Error");

});
```

Correct:

```
app.use((err, req, res, next) => {

    res.status(500).json({
        message: err.message
    });

});
```

## 12. ✅ Best Practices

1. Register middleware in the correct order.
2. Keep middleware functions small and reusable.
3. Use `return` when sending an early response.
4. Validate incoming request data.
5. Never expose passwords or secret tokens in logs.
6. Use environment variables for sensitive configuration.
7. Use centralized error-handling middleware.
8. Apply authentication middleware to protected routes.
9. Use third-party middleware when it provides reliable functionality.
10. Give middleware meaningful names.

### Recommended middleware order

```
const express = require("express");

const cors = require("cors");

const morgan = require("morgan");

const app = express();

// 1. Third-party middleware
app.use(cors());
app.use(morgan("dev"));

// 2. Built-in middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// 3. Custom middleware
app.use((req, res, next) => {

    console.log("Request received");

    next();

});

// 4. Routes
app.get("/", (req, res) => {

    res.send("Home Page");

});

// 5. Error handler
app.use((err, req, res, next) => {

    res.status(500).json({
        message: "Internal Server Error"
    });

});

app.listen(3000);
```

## 13. 🎯 Interview Questions

### Beginner Level

### Intermediate Level

### Advanced Level

## 14. 📝 Practice Problems

Try these problems in VS Code.

### Beginner Level

- Create middleware that prints `"Welcome to Express"`.
- Create middleware that prints the current date and time.
- Create middleware that displays the HTTP method.
- Create middleware that displays the request URL.

### Intermediate Level

- Create a logger middleware for all routes.
- Create authentication middleware using an environment variable.
- Create validation middleware for a student API.
- Create router-level middleware for a book module.

### Advanced Level

- Create a middleware that checks the user's role.
- Create middleware that checks whether an API key exists.
- Create centralized error-handling middleware.
- Build a complete Book Management API using multiple middleware functions.

## 15. 🏆 Mini Challenge — Student Management API

Your turn — don't look for the solution yet!

Requirement: Build a Student Management API using Express middleware.

Your API should contain:

1. A logger middleware.
2. JSON parsing middleware.
3. Student validation middleware.
4. Authentication middleware.
5. A POST `/students` route.
6. A GET `/students` route.

### Step 1 — Understand the requirement

We need to create a student API and protect the POST route using middleware.

### Step 2 — Input

Example POST request:

```
{
    "name": "Ramesh",
    "email": "ramesh@example.com",
    "course": "Node.js"
}
```

### Step 3 — Expected output

```
{
    "message": "Student created successfully"
}
```

### Step 4 — Break into steps

```
CLIENT
  |
  v
LOGGER MIDDLEWARE
  |
  v
JSON MIDDLEWARE
  |
  v
AUTHENTICATION MIDDLEWARE
  |
  v
VALIDATION MIDDLEWARE
  |
  v
POST /students
  |
  v
RESPONSE
```

### Step 5 — Hint

You need these functions:

```
function logger(req, res, next) {

    // Your code

}

function authenticate(req, res, next) {

    // Your code

}

function validateStudent(req, res, next) {

    // Your code

}
```

### Step 6 — Pseudocode

```
START

Create Express application

Register JSON middleware

Create logger middleware

Create authentication middleware

Create validation middleware

Create POST /students route

Create GET /students route

Start server

END
```

### Step 7 — Your turn

Try to write the code yourself.

- Created Express server.
- Created logger middleware.
- Created authentication middleware.
- Created validation middleware.
- Created POST route.
- Created GET route.
- Tested using Postman.

Send your code here. I will review it line by line, correct mistakes, and explain the logic.

## 16. 📌 Chapter Summary

| Concept            | What you learned                                |
| ------------------ | ----------------------------------------------- |
| Middleware         | Function executed during request-response cycle |
| `req`              | Client request information                      |
| `res`              | Sends a response                                |
| `next()`           | Passes control forward                          |
| `app.use()`        | Registers application middleware                |
| `router.use()`     | Registers router middleware                     |
| `express.json()`   | Parses JSON request body                        |
| `express.static()` | Serves static files                             |
| `cors`             | Handles cross-origin resource sharing           |
| Logger             | Records request information                     |
| Authentication     | Checks user credentials or tokens               |
| Validation         | Checks incoming data                            |
| Error middleware   | Handles application errors                      |

Most important concept: Middleware processes a request before it reaches the route handler, unless the middleware itself sends the response or passes an error.

## 17. ⚡ Quick Revision

### Chapter 19 Completion Checklist

- I understand middleware.
- I understand `req`, `res`, and `next`.
- I understand the request lifecycle.
- I understand all middleware types.
- I can create logger middleware.
- I can create authentication middleware.
- I can create validation middleware.
- I can create error-handling middleware.

Chapter 19 completed!

Next: Chapter 20 — Express Router

You will learn:

1. What is Express Router?
2. Why do we need Router?
3. `express.Router()`
4. Creating separate route files.
5. Connecting routes with `app.use()`.
6. Route parameters in Router.
7. Router-level middleware.
8. Building a modular Book API.
9. Professional folder structure.

When you're ready, type `NEXT` to start Chapter 20.