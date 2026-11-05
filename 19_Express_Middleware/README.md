# Chapter 19 — Express Middleware



PART 5 — EXPRESS.JS

Beginner to Advanced



## 🔑 Requires Before Starting

Before learning middleware, you should understand these Express basics:

1. Express server: An application created using `express()`.
2. Routing: Handling requests using `app.get()`, `app.post()`, etc.
3. Request (`req`): Contains information sent by the client.
4. Response (`res`): Used to send a response to the client.
5. JavaScript functions: Middleware is simply a function.
6. `next()`: A function that passes control to the next middleware or route handler.

Example:

```
const express = require("express");

const app = express();

app.get("/", (req, res) => {
    res.send("Hello Express");
});

app.listen(3000);
```

## 1. What is Middleware?

Middleware is a function that runs between receiving a client request and sending a response.

It can perform tasks such as:

- Logging request details.
- Checking user authentication.
- Validating request data.
- Reading JSON request bodies.
- Handling errors.
- Checking user permissions.

### Simple example

```
const myMiddleware = (req, res, next) => {
    console.log("Middleware is running");

    next();
};
```

Here:

- `req` — Contains request information.
- `res` — Allows us to send a response.
- `next` — Passes control to the next middleware or handler.

### 📖 Read

📖 Read — Understand middleware

### 💡 Important

💡 Important — Remember

## 2. Why do we need Middleware?

Consider a Student Management API.

Suppose you have 20 API routes:

```
GET     /students
POST    /students
GET     /students/:id
PUT     /students/:id
DELETE  /students/:id

GET     /teachers
POST    /teachers
GET     /teachers/:id
PUT     /teachers/:id
DELETE  /teachers/:id
```

You want to check whether a user is authenticated before accessing protected routes.

Without middleware, you might repeat authentication code inside every route.

```
app.get("/students", (req, res) => {
    // Authentication code

    res.json({ message: "Students" });
});

app.get("/teachers", (req, res) => {
    // Same authentication code again

    res.json({ message: "Teachers" });
});
```

This creates duplicate code.

With middleware:

```
const authMiddleware = (req, res, next) => {
    console.log("Checking authentication");

    next();
};

app.use(authMiddleware);
```

Now the middleware can be reused across multiple routes.

### Main benefits

1. Code reusability.
2. Better code organization.
3. Authentication and authorization.
4. Request validation.
5. Centralized logging.
6. Easier error handling.

## 3. Real-world analogy

Imagine entering an airport.

[Sûreté aéroportuaire : complémentarité entre sécurité et prévention QHSE](https://images.openai.com/static-rsc-4/GBKMebUxxKoO1We1CTxupFrHSD03wvFRI1MqYR_vTp7jk86pGTLcg0uo9r_GURhB6jYI-3NZos4hp11hbily2TNL7Vz1wpfC1tjbWzV7Q2uaShq1ISpi6UwGLtLFHFkCIH3DA04DcSupdD7-6pxnMbVPyrCbFq961iZ0XSiex4o?purpose=inline)

[qhselib.com](https://www.qhselib.com/actualites/surete-aeroportuaire-complementarite-entre-securite?utm_source=chatgpt.com)

The process:

1. You arrive at the airport.
2. Security checks your identity.
3. Your luggage is scanned.
4. You pass security.
5. You enter the departure area.

Express middleware works in a similar way.

| Airport           | Express                   |
| ----------------- | ------------------------- |
| Passenger         | Client request            |
| Identity check    | Authentication middleware |
| Luggage scan      | Validation middleware     |
| Security approval | `next()`                  |
| Departure area    | Route handler             |
| Final result      | Response                  |

## 4. Architecture / Flow

### Express request lifecycle

Client Request

Browser / Postman / React

Application Middleware

Logger, JSON parser

Router Middleware

Authentication, validation

Route Handler

Business logic

Response

JSON / Text / Status code

### Middleware flow diagram for GitHub README

Save this Mermaid diagram directly in your README. GitHub supports Mermaid diagrams.

\#chatgpt-mermaid-\_r_58a\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_58a\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_58a\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_58a\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_58a\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_58a\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_58a\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_58a\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_58a\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_58a\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_58a\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_58a\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_58a\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_58a\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_58a\_ p{margin:0;}#chatgpt-mermaid-\_r_58a\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_58a\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_58a\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_58a\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_58a\_ .label text,#chatgpt-mermaid-\_r_58a\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_58a\_ .node rect,#chatgpt-mermaid-\_r_58a\_ .node circle,#chatgpt-mermaid-\_r_58a\_ .node ellipse,#chatgpt-mermaid-\_r_58a\_ .node polygon,#chatgpt-mermaid-\_r_58a\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_58a\_ .rough-node .label text,#chatgpt-mermaid-\_r_58a\_ .node .label text,#chatgpt-mermaid-\_r_58a\_ .image-shape .label,#chatgpt-mermaid-\_r_58a\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_58a\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_58a\_ .rough-node .label,#chatgpt-mermaid-\_r_58a\_ .node .label,#chatgpt-mermaid-\_r_58a\_ .image-shape .label,#chatgpt-mermaid-\_r_58a\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_58a\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_58a\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_58a\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_58a\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_58a\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_58a\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_58a\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_58a\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_58a\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_58a\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_58a\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_58a\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_58a\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_58a\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_58a\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_58a\_ .icon-shape,#chatgpt-mermaid-\_r_58a\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_58a\_ .icon-shape p,#chatgpt-mermaid-\_r_58a\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_58a\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_58a\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_58a\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_58a\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_58a\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_58a\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_58a\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_58a\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_58a\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_58a\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_58a\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_58a\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_58a\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_58a\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_58a\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_58a\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_58a\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_58a\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_58a\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_58a\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_58a\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_58a\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_58a\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_58a\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_58a\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_58a\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_58a\_ .node rect,#chatgpt-mermaid-\_r_58a\_ .node circle,#chatgpt-mermaid-\_r_58a\_ .node ellipse,#chatgpt-mermaid-\_r_58a\_ .node polygon,#chatgpt-mermaid-\_r_58a\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_58a\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_58a\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_58a\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_58a\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_58a\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Client RequestApplication MiddlewareRouter MiddlewareRoute HandlerSend ResponseError MiddlewareError Responsenextnextnext errornext errornext error

### Understanding `next()`

There are three important possibilities:

| Code         | Meaning                                    |
| ------------ | ------------------------------------------ |
| `next()`     | Continue to the next middleware or handler |
| `next(err)`  | Pass an error to error-handling middleware |
| `res.send()` | Send a response and finish the request     |

Remember: Do not call `next()` after sending a response unless you intentionally want to pass control to another handler. Otherwise, you can cause errors such as trying to send a response twice.

## 5. Syntax

### Basic middleware syntax

```
const middlewareName = (req, res, next) => {

    // Perform some operation

    next();
};
```

### Register middleware

```
app.use(middlewareName);
```

### Register middleware for a particular route

```
app.get("/students", middlewareName, (req, res) => {

    res.send("Student List");

});
```

### Register multiple middleware functions

```
app.get(
    "/students",
    middlewareOne,
    middlewareTwo,
    (req, res) => {

        res.send("Students");

    }
);
```

Execution order:

```
middlewareOne
      ↓
middlewareTwo
      ↓
Route Handler
      ↓
Response
```

## 6. Basic Example

Let's create your first Express middleware.

### Project setup

```
19_Express_Middleware/
│
├── node_modules/
├── package.json
└── server.js
```

### Step 1: Install Express

```
npm init -y
npm install express
```

### Step 2: Create `server.js`

```
const express = require("express");

const app = express();

// Custom middleware
const myMiddleware = (req, res, next) => {

    console.log("Middleware executed");

    next();

};

// Register middleware
app.use(myMiddleware);

// Route
app.get("/", (req, res) => {

    res.send("Hello from Express");

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

Open:

```
http://localhost:3000
```

## 7. Dry Run

Let's understand what happens when you open `http://localhost:3000`.

| Step | Execution                | Result             |
| ---- | ------------------------ | ------------------ |
| 1    | Client sends GET request | Request received   |
| 2    | `app.use(myMiddleware)`  | Middleware runs    |
| 3    | `console.log()`          | Logs message       |
| 4    | `next()`                 | Passes control     |
| 5    | `app.get("/")`           | Route handler runs |
| 6    | `res.send()`             | Response sent      |

The important execution order is:

```
Client Request
      ↓
myMiddleware()
      ↓
console.log()
      ↓
next()
      ↓
app.get("/")
      ↓
res.send()
      ↓
Client receives response
```

## 8. Output

### VS Code terminal

```
Server running on port 3000
Middleware executed
```

### Browser

```
Hello from Express
```

Every time you refresh the browser, the middleware executes again.

## 9. Line-by-line explanation

Consider this code:

```
const myMiddleware = (req, res, next) => {

    console.log("Middleware executed");

    next();

};
```

| Code                 | Explanation                           |
| -------------------- | ------------------------------------- |
| `const myMiddleware` | Creates a middleware function         |
| `req`                | Contains incoming request information |
| `res`                | Allows us to send a response          |
| `next`               | Passes control to the next function   |
| `console.log()`      | Prints a message in the terminal      |
| `next()`             | Continues the request lifecycle       |

### What happens if we remove `next()`?

```
const myMiddleware = (req, res, next) => {

    console.log("Middleware executed");

    // No next()
    // No response

};
```

Result:

- Middleware executes.
- Route handler does not execute.
- No response is sent.
- Browser keeps waiting until the request times out or is otherwise terminated.

This is a common beginner mistake.

## 10. Practical example

Now let's understand the important types of Express middleware.

### 10.1 Application-level middleware

Application-level middleware is registered using `app.use()`.

It can execute for many routes in the application.

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

app.get("/about", (req, res) => {

    res.send("About Page");

});

app.listen(3000);
```

Both `/` and `/about` pass through the middleware.

Important: `app.use()` without a path generally matches all request paths. You can also provide a path to limit where it runs.

```
app.use("/admin", middlewareName);
```

This middleware applies to matching `/admin` paths.

### 10.2 Router-level middleware

Router-level middleware is registered on an Express Router.

It is useful when you want middleware to apply only to a particular group of routes.

Example structure:

```
19_Express_Middleware/
│
├── server.js
└── routes/
    └── studentRoutes.js
```

routes/studentRoutes.js

```
const express = require("express");

const router = express.Router();

// Router-level middleware
router.use((req, res, next) => {

    console.log("Student router middleware");

    next();

});

router.get("/", (req, res) => {

    res.json({
        message: "Student List"
    });

});

router.get("/:id", (req, res) => {

    res.json({
        message: "Student Details",
        id: req.params.id
    });

});

module.exports = router;
```

server.js

```
const express = require("express");

const app = express();

const studentRoutes = require("./routes/studentRoutes");

// Mount router
app.use("/students", studentRoutes);

app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Test:

```
GET /students
GET /students/101
```

Both requests pass through the student router middleware.

### 10.3 Built-in middleware

Express provides some middleware functions directly.

Three important built-in middleware functions are:

| Middleware             | Purpose                                          |
| ---------------------- | ------------------------------------------------ |
| `express.json()`       | Reads JSON request bodies                        |
| `express.urlencoded()` | Reads URL-encoded form data                      |
| `express.static()`     | Serves static files such as images, CSS and HTML |

A. `express.json()`

Suppose Postman sends:

```
{
    "name": "Ramesh",
    "age": 25
}
```

To access this data, use:

```
app.use(express.json());

app.post("/students", (req, res) => {

    console.log(req.body);

    res.json({
        message: "Student received",
        student: req.body
    });

});
```

Without JSON parsing middleware, `req.body` may be `undefined` for JSON requests.

B. `express.urlencoded()`

This middleware parses URL-encoded form submissions.

```
app.use(express.urlencoded({
    extended: true
}));
```

C. `express.static()`

This middleware makes static files available to clients.

```
app.use(express.static("public"));
```

Project structure:

```
project/
│
├── public/
│   ├── index.html
│   └── images/
│       └── logo.png
│
└── server.js
```

Now:

```
http://localhost:3000/index.html
http://localhost:3000/images/logo.png
```

The files can be accessed through the server.

### 10.4 Third-party middleware

Third-party middleware is created by external developers and installed using NPM.

Two popular examples:

| Package  | Purpose                        |
| -------- | ------------------------------ |
| `cors`   | Controls cross-origin requests |
| `morgan` | Logs HTTP request details      |

Install:

```
npm install cors morgan
```

Example:

```
const express = require("express");
const cors = require("cors");
const morgan = require("morgan");

const app = express();

// Third-party middleware
app.use(cors());

app.use(morgan("dev"));

app.use(express.json());

app.get("/", (req, res) => {

    res.json({
        message: "Hello API"
    });

});

app.listen(3000);
```

What does CORS do?

Imagine:

- React frontend runs on `http://localhost:5173`.
- Express backend runs on `http://localhost:3000`.

These are different origins because their ports are different.

CORS controls which origins are allowed to access your backend from browsers.

For a real application, configure allowed origins instead of blindly allowing every origin.

### 10.5 Error-handling middleware

Error middleware handles errors that occur during request processing.

Its function signature has four parameters:

```
(err, req, res, next)
```

Example:

```
const errorMiddleware = (err, req, res, next) => {

    console.error(err.message);

    res.status(500).json({
        message: "Internal Server Error"
    });

};
```

Register it after your routes:

```
app.use(errorMiddleware);
```

A complete example:

```
const express = require("express");

const app = express();

app.get("/error", (req, res, next) => {

    const error = new Error("Something went wrong");

    next(error);

});

// Error-handling middleware
app.use((err, req, res, next) => {

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

Expected response:

```
{
    "message": "Something went wrong"
}
```

Remember: Error-handling middleware uses four arguments. Keep all four parameters in the correct order.

### 10.6 Custom middleware

Custom middleware means middleware that you write yourself to solve a particular application requirement.

Let's build three useful examples.

A. Logger middleware

Purpose: Record every incoming request.

```
const loggerMiddleware = (req, res, next) => {

    // Get current date and time
    const time = new Date().toISOString();

    // Print HTTP method, URL and time
    console.log(
        req.method,
        req.originalUrl,
        time
    );

    next();

};

module.exports = loggerMiddleware;
```

Example terminal output:

```
GET /students 2026-11-06T10:30:00.000Z
POST /students 2026-11-06T10:31:00.000Z
```

Use it:

```
const loggerMiddleware = require("./middlewares/logger");

app.use(loggerMiddleware);
```

B. Authentication middleware

Purpose: Check whether the request contains an authentication token.

For this learning example, we will compare a token from an environment variable. This is only an illustration, not production-grade token verification.

Install:

```
npm install dotenv
```

Create `.env`:

```
API_TOKEN=learning-token-123
```

Add `.env` to `.gitignore`:

```
node_modules/
.env
```

Create `middlewares/authMiddleware.js`:

```
const authMiddleware = (req, res, next) => {

    // Read token from request header
    const token = req.headers.authorization;

    // Read expected token from environment
    const expectedToken = process.env.API_TOKEN;

    // Check whether token exists and matches
    if (!token || token !== `Bearer ${expectedToken}`) {

        return res.status(401).json({
            message: "Unauthorized access"
        });

    }

    // Allow request to continue
    next();

};

module.exports = authMiddleware;
```

Use it in `server.js`:

```
require("dotenv").config();

const express = require("express");
const authMiddleware = require("./middlewares/authMiddleware");

const app = express();

app.get("/profile", authMiddleware, (req, res) => {

    res.json({
        message: "Welcome to your profile"
    });

});

app.listen(3000);
```

Postman header:

```
Key: Authorization
Value: Bearer learning-token-123
```

If the token is correct, you receive:

```
{
    "message": "Welcome to your profile"
}
```

If it is missing or incorrect:

```
{
    "message": "Unauthorized access"
}
```

💡 Production security note

Comparing a token string is only a teaching example. Real applications should verify signed JWTs using a trusted library or validate a server-side session. Do not store real secrets in source code or commit `.env` to GitHub.

C. Validation middleware

Purpose: Check whether required data exists before sending it to the route handler.

Create `middlewares/validateStudent.js`:

```
const validateStudent = (req, res, next) => {

    // Extract student details
    const { name, email } = req.body;

    // Check required fields
    if (!name || !email) {

        return res.status(400).json({
            message: "Name and email are required"
        });

    }

    // Data is valid; continue
    next();

};

module.exports = validateStudent;
```

Use it:

```
const express = require("express");

const app = express();

const validateStudent = require("./middlewares/validateStudent");

app.use(express.json());

app.post("/students", validateStudent, (req, res) => {

    res.status(201).json({
        message: "Student created",
        student: req.body
    });

});

app.listen(3000);
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
    "message": "Student created",
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
    "message": "Name and email are required"
}
```

### 10.7 Middleware types — Quick comparison

| Type           | Registration       | Example                       |
| -------------- | ------------------ | ----------------------------- |
| Application    | `app.use()`        | Logger                        |
| Router         | `router.use()`     | Student router authentication |
| Built-in       | `express.*`        | `express.json()`              |
| Third-party    | `app.use(package)` | `cors`, `morgan`              |
| Error-handling | `app.use()`        | Central error handler         |
| Custom         | Your own function  | Validation                    |

### 10.8 Async middleware and Express versions

Modern Express applications may use asynchronous middleware.

Express 5: Rejected promises returned by async route handlers and middleware are automatically forwarded to error handling.

```
app.get("/students", async (req, res) => {

    const students = await getStudentsFromDatabase();

    res.json(students);

});
```

If `getStudentsFromDatabase()` rejects, Express 5 forwards the error.

Express 4: You generally need to catch the error and call `next(error)`, or use an appropriate async wrapper.

```
app.get("/students", async (req, res, next) => {

    try {

        const students = await getStudentsFromDatabase();

        res.json(students);

    } catch (error) {

        next(error);

    }

});
```

Check your installed Express version:

```
npm list express
```

## 11. Common mistakes

### Mistake 1 — Forgetting `next()`

Wrong:

```
app.use((req, res, next) => {

    console.log("Middleware");

});
```

Correct:

```
app.use((req, res, next) => {

    console.log("Middleware");

    next();

});
```

### Mistake 2 — Sending response twice

Wrong:

```
app.use((req, res, next) => {

    res.send("Hello");

    next();

});
```

The next handler might attempt to send another response.

Correct:

```
app.use((req, res, next) => {

    res.send("Hello");

});
```

### Mistake 3 — Incorrect middleware order

Wrong:

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

The JSON parser must be registered before the routes that need it.

### Mistake 4 — Incorrect error middleware signature

Wrong:

```
app.use((err, req, res) => {

    res.status(500).send("Error");

});
```

Correct:

```
app.use((err, req, res, next) => {

    res.status(500).send("Error");

});
```

### Mistake 5 — Using `next()` after responding

Wrong:

```
if (!token) {

    res.status(401).send("Unauthorized");

    next();

}
```

Correct:

```
if (!token) {

    return res.status(401).send("Unauthorized");

}

next();
```

## 12. Best practices

1. Keep middleware in a separate `middlewares/` folder.
2. Give each middleware one responsibility.
3. Register middleware in the correct order.
4. Use `return` when sending an early response.
5. Use environment variables for secrets.
6. Validate user input before processing it.
7. Use centralized error handling.
8. Do not expose sensitive error details to clients.
9. Use third-party middleware only when needed.
10. Avoid writing duplicate middleware code.

### Recommended professional project structure

```
19_Express_Middleware/
│
├── middlewares/
│   ├── logger.js
│   ├── authMiddleware.js
│   ├── validateStudent.js
│   └── errorMiddleware.js
│
├── routes/
│   └── studentRoutes.js
│
├── public/
│   └── images/
│
├── .env
├── .gitignore
├── package.json
└── server.js
```

### GitHub README image folder

If you later add your own diagrams or handwritten notes, organize them like this:

```
19_Express_Middleware/
│
├── images/
│   ├── middleware-flow.png
│   ├── middleware-types.png
│   └── request-lifecycle.png
│
└── README.md
```

Use relative paths in GitHub:

```
![Middleware Flow](./images/middleware-flow.png)

![Middleware Types](./images/middleware-types.png)
```

These image files must actually exist in your repository. The Mermaid diagrams in this chapter can be pasted directly into your README without creating image files.

## 13. Interview questions

### Beginner level

Q1. What is middleware in Express.js?

Middleware is a function that runs during the request-response lifecycle. It can process a request, send a response, or pass control to another middleware using `next()`.

Q2. What are `req`, `res`, and `next`?

- `req`: Request information.
- `res`: Used to send the response.
- `next`: Passes control to the next middleware or handler.

Q3. What is `app.use()`?

`app.use()` registers middleware at the application level.

Q4. What is `express.json()`?

It is built-in middleware that parses incoming JSON request bodies.

### Intermediate level

Q5. What is the difference between application-level and router-level middleware?

Application-level middleware is registered using `app.use()`. Router-level middleware is registered using `router.use()` and can be limited to a particular router.

Q6. What happens if we don't call `next()`?

If the middleware neither sends a response nor passes control, the request remains pending.

Q7. What is error-handling middleware?

It is middleware designed to handle errors. It has four parameters:

```
(err, req, res, next)
```

Q8. What is third-party middleware?

Middleware developed outside Express and installed through NPM. Examples include `cors` and `morgan`.

### Advanced level

Q9. What is the difference between `next()` and `next(err)`?

- `next()` passes control normally.
- `next(err)` passes an error to Express error-handling middleware.

Q10. Why is middleware order important?

Middleware executes in registration order. For example, the JSON parser must run before routes that need to access `req.body`.

Q11. How do you protect routes using authentication middleware?

Create middleware that verifies a user's session or token. If valid, call `next()`. Otherwise, return an unauthorized response.

Q12. How does Express 5 handle rejected async middleware promises?

Express 5 automatically forwards rejected promises from returned async middleware and route-handler functions to error-handling middleware.

## 14. Practice problems

Try these exercises yourself before looking for a solution.

### Beginner exercises

1. Create a middleware that prints `Welcome to Middleware`.
2. Create a middleware that logs the HTTP request method.
3. Create middleware that logs the requested URL.
4. Create middleware that logs the current date and time.
5. Apply middleware to two different routes.

### Intermediate exercises

6. Create a logger middleware in a separate file.
7. Create a validation middleware for student name and email.
8. Create an authentication middleware that checks an Authorization header.
9. Create router-level middleware for student routes.
10. Create error-handling middleware.

### Advanced exercises

11. Build an API with logger and authentication middleware.
12. Apply validation middleware only to POST routes.
13. Build an admin route protected by authentication middleware.
14. Create a reusable middleware for checking user roles.
15. Build a centralized error-handling system.

## 15. Mini challenge — Employee Management API

Your task

Build an Employee API using middleware.

### Requirements

Create these routes:

```
GET     /employees
POST    /employees
GET     /employees/:id
```

Create these middleware files:

```
middlewares/
│
├── logger.js
├── auth.js
└── validateEmployee.js
```

### Expected behavior

1\. Logger middleware

Every request should print:

```
GET /employees
POST /employees
```

2\. Authentication middleware

Only allow requests with a valid Authorization header.

3\. Validation middleware

For POST requests, require:

```
{
    "name": "Ramesh",
    "email": "ramesh@example.com",
    "salary": 30000
}
```

If fields are missing, return:

```
{
    "message": "All employee fields are required"
}
```

4\. Expected project structure

```
19_Express_Middleware/
│
├── middlewares/
│   ├── logger.js
│   ├── auth.js
│   └── validateEmployee.js
│
├── routes/
│   └── employeeRoutes.js
│
├── server.js
└── package.json
```

Try building this independently. It will help you understand how middleware is used in real backend applications.

## 16. Chapter summary

| Topic                  | What you learned                      |
| ---------------------- | ------------------------------------- |
| Middleware             | Function between request and response |
| `req`                  | Request information                   |
| `res`                  | Response object                       |
| `next()`               | Passes control                        |
| Application middleware | `app.use()`                           |
| Router middleware      | `router.use()`                        |
| Built-in middleware    | `express.json()`                      |
| Third-party middleware | `cors`, `morgan`                      |
| Error middleware       | `(err, req, res, next)`               |
| Custom middleware      | Logger, authentication, validation    |

Main concept:

Middleware helps us write reusable, organized, secure, and maintainable Express applications.

## 17. Quick revision

🧠 Remember these important points

- Middleware executes during the request-response lifecycle.
- `next()` continues normal execution.
- `next(err)` forwards an error.
- `app.use()` registers application middleware.
- `router.use()` registers router middleware.
- `express.json()` parses JSON request bodies.
- Authentication checks who the user is.
- Validation checks whether the supplied data is acceptable.
- Error middleware has four parameters.
- Middleware order matters.

  ⭐ Most important syntax

```
app.use((req, res, next) => {

    console.log("Middleware");

    next();

});
```

Error middleware:

```
app.use((err, req, res, next) => {

    res.status(500).json({
        message: err.message
    });

});
```

Chapter 19 completed

Practice: First try the Employee Management API mini challenge. When you're ready, type `NEXT` to start Chapter 20 — Express Router.