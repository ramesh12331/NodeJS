# 🚀 PART 5 — EXPRESS.JS

# 📘 Chapter 17 — Introduction to Express.js

> Learning Goal: Understand Express.js from beginner level and create your first backend server using Node.js and Express.js.

## 📑 Table of Contents

1. What is Express.js?
2. Why do we need Express.js?
3. Node.js vs Express.js
4. Real-world Analogy
5. Architecture / Flow
6. Installing Express.js
7. Creating Express Server
8. app.listen()
9. Request and Response
10. Practical Example
11. Common Mistakes
12. Best Practices
13. Interview Questions
14. Practice Problems
15. Mini Challenge
16. Chapter Summary
17. Quick Revision

## 📘 1. What is Express.js?

### 🔹 Definition

Express.js is a lightweight web framework for Node.js that helps developers build web servers and REST APIs easily.

Understand these two concepts:

- Node.js: Allows JavaScript to run outside the browser.
- Express.js: Makes backend development easier using Node.js.

### 💡 Example

Suppose you are developing a Book Management Application.

You need these API endpoints:

```
GET     /api/books
POST    /api/books
PUT     /api/books/1
DELETE  /api/books/1
```

Express.js helps us create these API endpoints.

### 📌 Important Concepts

| Technology | Purpose              |
| ---------- | -------------------- |
| JavaScript | Programming language |
| Node.js    | JavaScript runtime   |
| Express.js | Web framework        |
| React.js   | Frontend library     |
| MongoDB    | NoSQL database       |
| PostgreSQL | Relational database  |

## 🎯 2. Why do we need Express.js?

Before Express.js, we could create servers using the Node.js built-in HTTP module.

### ❌ Without Express.js

```
// Import Node.js HTTP module
const http = require("http");

// Create HTTP server
const server = http.createServer((req, res) => {

    // Check requested URL
    if (req.url === "/") {

        // Send response
        res.write("Welcome to Node.js");

        // End response
        res.end();
    }

});

// Start server
server.listen(3000);
```

This works, but as applications grow, we need to write more code for:

- URL checking.
- HTTP method checking.
- Request body handling.
- Routing.
- Error handling.
- Middleware.

### ✅ With Express.js

```
// Import Express
const express = require("express");

// Create Express application
const app = express();

// Create GET route
app.get("/", (req, res) => {

    res.send("Welcome to Express.js");

});

// Start server
app.listen(3000);
```

Express.js makes backend development simpler and more organized.

### ⭐ Advantages of Express.js

| Feature              | Explanation                 |
| -------------------- | --------------------------- |
| Routing              | Easily create API endpoints |
| Middleware           | Process incoming requests   |
| Request handling     | Access client information   |
| Response handling    | Send JSON or text           |
| Error handling       | Manage application errors   |
| Database integration | Connect databases           |
| REST API             | Build backend services      |

## ⚖️ 3. Node.js vs Express.js

| Node.js                             | Express.js                             |
| ----------------------------------- | -------------------------------------- |
| JavaScript runtime                  | Web framework                          |
| Executes JavaScript outside browser | Runs on Node.js                        |
| Provides built-in modules           | Provides web application functionality |
| HTTP module creates servers         | Simplifies server creation             |
| Lower-level functionality           | Routing and middleware support         |

### 💻 Example

Node.js:

```
const http = require("http");
```

Express.js:

```
const express = require("express");
```

## 🌍 4. Real-world Analogy

Imagine a restaurant.

| Restaurant    | Backend        |
| ------------- | -------------- |
| Customer      | Client         |
| Waiter        | Express.js     |
| Kitchen       | Business logic |
| Storage room  | Database       |
| Food delivery | HTTP response  |

### 🔄 How it works

1. Customer orders food.
2. Waiter receives the order.
3. Kitchen prepares the food.
4. Waiter delivers the food.
5. Customer receives the food.

Backend equivalent:

1. React sends an API request.
2. Express receives the request.
3. Controller processes the request.
4. Database provides information.
5. Express sends a response.

Remember: Express acts as the middle layer between the client and backend processing.

## 🏗️ 5. Architecture / Flow

### Node.js + Express Architecture

```
┌───────────────────────────────────┐
│          REACT FRONTEND           │
│            Client Side            │
└─────────────────┬─────────────────┘
                  │
                  │ HTTP Request
                  ▼
┌───────────────────────────────────┐
│           NODE.JS RUNTIME         │
│       Executes JavaScript         │
└─────────────────┬─────────────────┘
                  │
                  ▼
┌───────────────────────────────────┐
│          EXPRESS SERVER           │
│       Handles HTTP Requests       │
└─────────────────┬─────────────────┘
                  │
                  ▼
┌───────────────────────────────────┐
│           EXPRESS ROUTER          │
│          Matches Routes           │
└─────────────────┬─────────────────┘
                  │
                  ▼
┌───────────────────────────────────┐
│             CONTROLLER            │
│          Handles Logic            │
└─────────────────┬─────────────────┘
                  │
                  ▼
┌───────────────────────────────────┐
│              DATABASE             │
│        MongoDB / PostgreSQL        │
└─────────────────┬─────────────────┘
                  │
                  ▼
┌───────────────────────────────────┐
│           HTTP RESPONSE           │
│            JSON / Data            │
└─────────────────┬─────────────────┘
                  │
                  ▼
           REACT FRONTEND
```

### 📌 Understand the flow

| Step | Component  | Responsibility            |
| ---- | ---------- | ------------------------- |
| 1    | React      | Sends HTTP request        |
| 2    | Node.js    | Executes JavaScript       |
| 3    | Express    | Receives request          |
| 4    | Router     | Identifies matching route |
| 5    | Controller | Processes request         |
| 6    | Database   | Stores or retrieves data  |
| 7    | Express    | Sends response            |

### 🔄 Request and Response Flow

```
             CLIENT
                │
                │ GET /api/books
                ▼
         EXPRESS SERVER
                │
                ▼
          EXPRESS ROUTER
                │
                ▼
           CONTROLLER
                │
                ▼
            DATABASE
                │
                │ Book Data
                ▼
           CONTROLLER
                │
                ▼
         EXPRESS RESPONSE
                │
                │ JSON Response
                ▼
              CLIENT
```

## ⚙️ 6. Installing Express.js

Let's create your first Express project in VS Code.

### Step 1: Create project folder

```
mkdir express-learning
```

### Step 2: Navigate into folder

```
cd express-learning
```

### Step 3: Initialize Node.js

```
npm init -y
```

This creates:

```
package.json
```

What is package.json?

It stores project information, dependencies and scripts.

### Step 4: Install Express

```
npm install express
```

### Step 5: Create server.js

Project structure:

```
express-learning/
│
├── node_modules/
│
├── package.json
│
├── package-lock.json
│
└── server.js
```

## 💻 7. Creating Your First Express Server

Create a file named server.js.

```
// Step 1: Import Express package
const express = require("express");

// Step 2: Create Express application
const app = express();

// Step 3: Create GET route
app.get("/", (req, res) => {

    // Step 4: Send response
    res.send("Welcome to my first Express Server!");

});

// Step 5: Start server on port 3000
app.listen(3000, () => {

    console.log("Server running at http://localhost:3000");

});
```

### ▶️ Run the server

```
node server.js
```

Expected terminal output:

```
Server running at http://localhost:3000
```

Open your browser:

```
http://localhost:3000
```

Expected output:

```
Welcome to my first Express Server!
```

### 🔍 Dry Run — How does this code execute?

| Step | Code                 | Explanation         |
| ---- | -------------------- | ------------------- |
| 1    | `require("express")` | Imports Express     |
| 2    | `express()`          | Creates application |
| 3    | `app.get()`          | Registers GET route |
| 4    | `/`                  | Defines home URL    |
| 5    | `req`                | Request object      |
| 6    | `res`                | Response object     |
| 7    | `res.send()`         | Sends response      |
| 8    | `app.listen()`       | Starts server       |

Important: The server keeps running and waits for incoming requests.

## 🔌 8. Understanding app.listen()

### 🔹 Definition

`app.listen()` starts the Express server and makes it listen for incoming HTTP requests on a specified port.

### Syntax

```
app.listen(PORT, callback);
```

### Example

```
app.listen(3000, () => {

    console.log("Server started successfully");

});
```

### Explanation

| Code           | Meaning                               |
| -------------- | ------------------------------------- |
| `app.listen()` | Starts server                         |
| `3000`         | Port number                           |
| `callback`     | Executes when server starts listening |

### What is a port?

A port is a communication endpoint used by applications to receive network traffic.

```
React Vite       → 5173
Express Server   → 3000
PostgreSQL       → 5432
MongoDB          → 27017
```

## 🔄 9. Understanding Request and Response

Two important Express objects:

- `req` — Request.
- `res` — Response.

### 📥 What is Request (`req`)?

A request contains information sent by the client to the backend server.

Examples:

- URL.
- HTTP method.
- Headers.
- Parameters.
- Query strings.
- Request body.

### 📤 What is Response (`res`)?

A response contains information sent from the backend server to the client.

### Example

```
app.get("/", (req, res) => {

    // Request information
    console.log(req.method);
    console.log(req.url);

    // Send response
    res.send("Hello Student");

});
```

Expected terminal output:

```
GET
/
```

Expected browser output:

```
Hello Student
```

### Difference between req and res

| Request (`req`)           | Response (`res`)           |
| ------------------------- | -------------------------- |
| Comes from client         | Goes to client             |
| Contains incoming data    | Sends outgoing data        |
| Reads request information | Sends response information |

### 🧠 Remember this concept

```
        CLIENT
           │
           │ REQUEST
           ▼
    EXPRESS SERVER
           │
           │ PROCESSING
           ▼
       RESPONSE
           │
           ▼
        CLIENT
```

## 🚀 10. Practical Example — Student Information Server

### Requirement

Create a simple Student Information API with four routes.

```
GET /
GET /students
GET /courses
GET /contact
```

### Code

Create `server.js`:

```
const express = require("express");

const app = express();

// Home route
app.get("/", (req, res) => {

    res.send("Welcome to Student API");

});

// Students route
app.get("/students", (req, res) => {

    res.send("Student Name: Ramesh");

});

// Courses route
app.get("/courses", (req, res) => {

    res.send("Node.js, Express.js, React.js");

});

// Contact route
app.get("/contact", (req, res) => {

    res.send("Contact: admin@example.com");

});

// Start server
app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

### 🧪 Test the endpoints

| URL                       | Expected output               |
| ------------------------- | ----------------------------- |
| `localhost:3000/`         | Welcome to Student API        |
| `localhost:3000/students` | Student Name: Ramesh          |
| `localhost:3000/courses`  | Node.js, Express.js, React.js |
| `localhost:3000/contact`  | Contact: admin\@example.com   |

### Visual execution flow

```
              CLIENT
                 │
                 ▼
        http://localhost:3000
                 │
                 ▼
          EXPRESS SERVER
                 │
                 ▼
          CHECK REQUEST URL
                 │
       ┌─────────┼──────────┐
       │         │          │
       ▼         ▼          ▼
    /students  /courses   /contact
       │         │          │
       ▼         ▼          ▼
   Student    Course      Contact
    Data       Data        Data
       │         │          │
       └─────────┼──────────┘
                 │
                 ▼
           HTTP RESPONSE
                 │
                 ▼
               CLIENT
```

## ⚠️ 11. Common Mistakes

### Mistake 1: Express not installed

Wrong:

```
node server.js
```

If Express is not installed, you may receive:

```
Error: Cannot find module 'express'
```

Correct:

```
npm install express
```

### Mistake 2: Forgetting parentheses

Wrong:

```
const app = express;
```

Correct:

```
const app = express();
```

### Mistake 3: Forgetting response

Wrong:

```
app.get("/", (req, res) => {

    console.log("Hello");

});
```

Correct:

```
app.get("/", (req, res) => {

    res.send("Hello");

});
```

### Mistake 4: Port already in use

If port 3000 is occupied, use another available port.

```
app.listen(3001);
```

### Mistake 5: Wrong URL

If you create:

```
app.get("/students", (req, res) => {

    res.send("Students");

});
```

Visit:

```
http://localhost:3000/students
```

## ⭐ 12. Best Practices

1. Use meaningful route names.
2. Use environment variables for configuration.
3. Separate routes and controllers.
4. Use middleware for common request processing.
5. Implement centralized error handling.
6. Validate incoming request data.
7. Never hard-code passwords or secrets.
8. Use appropriate HTTP status codes.
9. Keep code modular.
10. Use `async/await` for asynchronous operations.

### Professional Environment Configuration

Install dotenv:

```
npm install dotenv
```

Create `.env`:

```
PORT=3000
```

Update `server.js`:

```
// Load environment variables
require("dotenv").config();

const express = require("express");

const app = express();

// Read port from environment
const PORT = process.env.PORT || 3000;

// Create route
app.get("/", (req, res) => {

    res.send("Express Server Running");

});

// Start server
app.listen(PORT, () => {

    console.log(`Server running on port ${PORT}`);

});
```

Important: Add `.env` to `.gitignore` so private configuration is not committed to GitHub.

## 🎤 13. Interview Questions

### 🟢 Beginner Level

### 🟡 Intermediate Level

### 🔴 Advanced Level

## 📝 14. Practice Problems

Try these exercises independently.

| No. | Problem                            | Difficulty |
| --- | ---------------------------------- | ---------- |
| 1   | Create Express server on port 4000 | Easy       |
| 2   | Create `/home` route               | Easy       |
| 3   | Create `/about` route              | Easy       |
| 4   | Create `/services` route           | Easy       |
| 5   | Create `/student` route            | Medium     |
| 6   | Create `/products` route           | Medium     |
| 7   | Create five different GET routes   | Medium     |

## 🏆 15. Mini Challenge — Student Information Server

Your Task

Build a Student Information Server independently.

### Step 1 — Requirement

Create a server with four routes.

### Step 2 — Input

Client sends HTTP requests using browser URLs.

### Step 3 — Output

Server returns appropriate text responses.

### Step 4 — Break into small steps

1. Import Express.
2. Create Express application.
3. Create home route.
4. Create students route.
5. Create courses route.
6. Create contact route.
7. Start server.

### Step 5 — Hint

Use:

```
app.get()
```

### Step 6 — Pseudocode

```
START

Import Express

Create Express application

Create GET /

Create GET /students

Create GET /courses

Create GET /contact

Start server

END
```

### Step 7 — Your Turn

Write the code independently.

### Step 8–11 — Code Review

After you send your code, I will:

- Review your code.
- Correct mistakes.
- Show the professional solution.
- Perform a dry run.
- Explain how to improve your backend logic.

## 📚 16. Chapter Summary

| Concept        | Explanation                       |
| -------------- | --------------------------------- |
| Express.js     | Node.js web framework             |
| `express()`    | Creates application               |
| `app`          | Express application instance      |
| `app.get()`    | Handles GET requests              |
| `req`          | Request information               |
| `res`          | Response object                   |
| `res.send()`   | Sends response                    |
| `app.listen()` | Starts server                     |
| Port           | Network communication endpoint    |
| Routing        | Maps URLs and methods to handlers |

## ⚡ 17. Quick Revision

### Basic Express Server

```
const express = require("express");

const app = express();

app.get("/", (req, res) => {

    res.send("Hello Express");

});

app.listen(3000, () => {

    console.log("Server started");

});
```

### Important Commands

```
npm init -y
npm install express
node server.js
```

### Remember the Flow

```
┌───────────────────┐
│       CLIENT      │
└─────────┬─────────┘
          │
          │ HTTP REQUEST
          ▼
┌───────────────────┐
│   EXPRESS SERVER  │
└─────────┬─────────┘
          │
          ▼
┌───────────────────┐
│   ROUTE HANDLER   │
└─────────┬─────────┘
          │
          ▼
┌───────────────────┐
│  BUSINESS LOGIC   │
└─────────┬─────────┘
          │
          ▼
┌───────────────────┐
│  HTTP RESPONSE    │
└─────────┬─────────┘
          │
          ▼
       CLIENT
```

# ✅ Chapter 17 — Learning Progress

Track your progress while reading and practising.

- 📘 Understand Express.js
- 🎯 Understand why we need Express.js
- ⚖️ Node.js vs Express.js
- 🌍 Real-world analogy
- 🏗️ Architecture and request flow
- ⚙️ Install Express.js
- 💻 Create Express server
- 🔌 Understand `app.listen()`
- 🔄 Understand `req` and `res`
- 🚀 Create multiple routes
- ⚠️ Understand common mistakes
- ⭐ Understand best practices
- 🎤 Prepare interview questions
- 📝 Complete practice problems
- 🏆 Solve Student API mini challenge
- 📚 Revise chapter summary

## 🎯 Chapter 17 — Final Test

Chapter 17 — Completed

Next Chapter: Chapter 18 — Express Routing

Topics:

- `app.get()`
- `app.post()`
- `app.put()`
- `app.patch()`
- `app.delete()`
- Route parameters
- Query parameters
- Request body
- Route handlers

Type `NEXT` when you are ready.