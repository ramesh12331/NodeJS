# 🚀 PART 5 — EXPRESS.JS

# 📘 Chapter 17 — Introduction to Express.js

> Learning goal: Understand Express.js from the basics and create your first backend server using Node.js and Express.js.

## 📑 Table of Contents

- 1\. What is Express.js?
- 2\. Why Express.js?
- 3\. Node.js vs Express.js
- 4\. Real-world Analogy
- 5\. Architecture / Flow
- 6\. Installing Express.js
- 7\. Creating Express Server
- 8\. app.listen()
- 9\. Request and Response
- 10\. Practical Example
- 11\. Common Mistakes
- 12\. Best Practices
- 13\. Interview Questions
- 14\. Practice Problems
- 15\. Mini Challenge
- 16\. Chapter Summary
- 17\. Quick Revision

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

### 📌 Important points

| Technology | Purpose              |
| ---------- | -------------------- |
| JavaScript | Programming language |
| Node.js    | JavaScript runtime   |
| Express.js | Web framework        |
| React.js   | Frontend library     |
| MongoDB    | NoSQL database       |
| PostgreSQL | Relational database  |

## 🎯 2. Why do we need Express.js?

Before Express.js, we could create servers using Node.js built-in HTTP module.

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

## 🏗️ 5. Architecture / Flow

### Node.js + Express architecture

\#chatgpt-mermaid-\_r_8q5\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_8q5\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_8q5\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_8q5\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_8q5\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_8q5\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_8q5\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_8q5\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_8q5\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_8q5\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_8q5\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_8q5\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_8q5\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_8q5\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_8q5\_ p{margin:0;}#chatgpt-mermaid-\_r_8q5\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_8q5\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_8q5\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_8q5\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_8q5\_ .label text,#chatgpt-mermaid-\_r_8q5\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_8q5\_ .node rect,#chatgpt-mermaid-\_r_8q5\_ .node circle,#chatgpt-mermaid-\_r_8q5\_ .node ellipse,#chatgpt-mermaid-\_r_8q5\_ .node polygon,#chatgpt-mermaid-\_r_8q5\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_8q5\_ .rough-node .label text,#chatgpt-mermaid-\_r_8q5\_ .node .label text,#chatgpt-mermaid-\_r_8q5\_ .image-shape .label,#chatgpt-mermaid-\_r_8q5\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_8q5\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_8q5\_ .rough-node .label,#chatgpt-mermaid-\_r_8q5\_ .node .label,#chatgpt-mermaid-\_r_8q5\_ .image-shape .label,#chatgpt-mermaid-\_r_8q5\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_8q5\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_8q5\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_8q5\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_8q5\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_8q5\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_8q5\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_8q5\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_8q5\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_8q5\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_8q5\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_8q5\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_8q5\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_8q5\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_8q5\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_8q5\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_8q5\_ .icon-shape,#chatgpt-mermaid-\_r_8q5\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_8q5\_ .icon-shape p,#chatgpt-mermaid-\_r_8q5\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_8q5\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_8q5\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_8q5\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_8q5\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_8q5\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_8q5\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_8q5\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_8q5\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_8q5\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_8q5\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_8q5\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_8q5\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_8q5\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_8q5\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_8q5\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_8q5\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_8q5\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_8q5\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_8q5\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_8q5\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_8q5\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_8q5\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_8q5\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_8q5\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_8q5\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_8q5\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_8q5\_ .node rect,#chatgpt-mermaid-\_r_8q5\_ .node circle,#chatgpt-mermaid-\_r_8q5\_ .node ellipse,#chatgpt-mermaid-\_r_8q5\_ .node polygon,#chatgpt-mermaid-\_r_8q5\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_8q5\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_8q5\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_8q5\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_8q5\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_8q5\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Client / React ApplicationNode.js RuntimeExpress ApplicationExpress RouterRoute HandlerBusiness LogicDatabaseHTTP RequestHTTP Response

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

Create a file named `server.js`.

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

### Professional environment configuration

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

Your task

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

### Step 7 — Your turn

Write the code independently.

### Step 8–11 — Code review

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

### Basic Express server

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

### Important commands

```
npm init -y
npm install express
node server.js
```

### Remember the flow

```
Client
   |
   | HTTP Request
   v
Express Server
   |
   v
Route Handler
   |
   v
Business Logic
   |
   v
HTTP Response
   |
   v
Client
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

Next: Chapter 18 — Express Routing

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