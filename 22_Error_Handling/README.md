# Chapter 22 — Express Error Handling



PART 5 — EXPRESS.JS

Beginner to Advanced



## 🔑 Requires Before Starting

Before learning error handling, you should understand:

1. Node.js: JavaScript runtime used for backend development.
2. Express.js: Framework used to create APIs.
3. Routing: Handling HTTP requests using `GET`, `POST`, `PUT`, and `DELETE`.
4. Middleware: Functions that execute during the request-response lifecycle.
5. Express Router: Separating routes into different files.
6. Controllers: Functions that handle incoming requests and send responses.
7. JavaScript functions: Understanding function calls, callbacks, and `try/catch`.
8. HTTP status codes: Understanding codes such as `200`, `201`, `400`, `401`, `404`, and `500`.

Example:

```
app.get("/students", (req, res) => {

    res.status(200).json({
        message: "Students fetched successfully"
    });

});
```

## 1. What is Error Handling?

Error handling is the process of detecting errors in an application and responding to them properly.

Errors can happen for many reasons:

- User enters invalid data.
- Requested student does not exist.
- Database connection fails.
- Authentication token is invalid.
- Server encounters an unexpected problem.

Instead of allowing the application to crash or return confusing messages, we handle errors and send meaningful responses.

### Simple example without error handling

```
app.get("/students/:id", (req, res) => {

    const student = undefined;

    res.json(student.name);

});
```

This code produces an error because we are trying to access `name` from `undefined`.

### Correct example

```
app.get("/students/:id", (req, res) => {

    const student = undefined;

    if (!student) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    res.json(student);

});
```

Now the application sends a meaningful error response.

### 📖 Read

📖 Read — Understand error handling

### 💡 Important

💡 Important — Remember

## 2. Why do we need Error Handling?

Imagine your Student Management API has these operations:

```
GET     /students
POST    /students
GET     /students/:id
PUT     /students/:id
DELETE  /students/:id
```

Different errors can occur.

| Situation                 | Error                 |
| ------------------------- | --------------------- |
| Student ID does not exist | Student not found     |
| Name is missing           | Validation error      |
| Token is invalid          | Unauthorized          |
| Database is unavailable   | Database error        |
| Unexpected server problem | Internal server error |

Without error handling:

- The application may crash.
- Users may receive confusing responses.
- Sensitive information might be exposed.
- Debugging becomes difficult.
- Frontend developers cannot handle API errors consistently.

### Benefits

1. Prevent unexpected application crashes where errors can be handled.
2. Send meaningful messages to users.
3. Use correct HTTP status codes.
4. Protect sensitive information.
5. Make debugging easier.
6. Centralize error-handling logic.

## 3. Real-world analogy

[Notdienst in Mülheim: Patientenversorgung wird verändert](https://images.openai.com/static-rsc-4/JPZVhuPSs9r698A7YzrALLq5HPd_D9yjoXaOKkaaQ2winPhhwCNNi7VKGyykZzZN_TbXi6gLB_h33Aa3hOGgqRM12MIi2pKkCneswX8wYZR3MJ603echn7geSSMfKJ4M_v_Znr3_qolS0Glh8L_51I-XhVSphgsSHCHG3W3dUH8?purpose=inline)

[waz.de](https://www.waz.de/staedte/muelheim/article242399670/Notdienstpraxis-zieht-um-Unnoetige-Wartezeiten-vermeiden.html?utm_source=chatgpt.com)

Imagine visiting a hospital.

1. You explain your problem.
2. The receptionist identifies the issue.
3. The receptionist directs you to the correct department.
4. The doctor checks the problem.
5. You receive the appropriate treatment.

Similarly, Express error handling:

| Hospital            | Express                   |
| ------------------- | ------------------------- |
| Patient problem     | Application error         |
| Receptionist        | Error detection           |
| Correct department  | Error handling middleware |
| Doctor checks issue | Error processing          |
| Treatment           | Error response            |

## 4. Architecture / Flow

### Express error-handling lifecycle

Client Request

Browser / Postman / React

Express Router

Controller

Process request

Success

Send response

Error

Pass error

Success Response

Error Middleware

Error Response

### GitHub Mermaid diagram

Copy this directly into your README.

\#chatgpt-mermaid-\_r_6h3\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_6h3\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_6h3\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_6h3\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_6h3\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6h3\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_6h3\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_6h3\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_6h3\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_6h3\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_6h3\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_6h3\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_6h3\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_6h3\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_6h3\_ p{margin:0;}#chatgpt-mermaid-\_r_6h3\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6h3\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6h3\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6h3\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_6h3\_ .label text,#chatgpt-mermaid-\_r_6h3\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6h3\_ .node rect,#chatgpt-mermaid-\_r_6h3\_ .node circle,#chatgpt-mermaid-\_r_6h3\_ .node ellipse,#chatgpt-mermaid-\_r_6h3\_ .node polygon,#chatgpt-mermaid-\_r_6h3\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_6h3\_ .rough-node .label text,#chatgpt-mermaid-\_r_6h3\_ .node .label text,#chatgpt-mermaid-\_r_6h3\_ .image-shape .label,#chatgpt-mermaid-\_r_6h3\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_6h3\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_6h3\_ .rough-node .label,#chatgpt-mermaid-\_r_6h3\_ .node .label,#chatgpt-mermaid-\_r_6h3\_ .image-shape .label,#chatgpt-mermaid-\_r_6h3\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_6h3\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_6h3\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_6h3\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_6h3\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_6h3\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_6h3\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_6h3\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_6h3\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_6h3\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_6h3\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_6h3\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6h3\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6h3\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_6h3\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6h3\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_6h3\_ .icon-shape,#chatgpt-mermaid-\_r_6h3\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_6h3\_ .icon-shape p,#chatgpt-mermaid-\_r_6h3\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_6h3\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_6h3\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_6h3\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_6h3\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_6h3\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_6h3\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_6h3\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_6h3\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_6h3\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_6h3\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_6h3\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_6h3\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_6h3\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_6h3\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_6h3\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_6h3\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_6h3\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_6h3\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_6h3\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_6h3\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_6h3\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_6h3\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_6h3\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_6h3\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_6h3\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_6h3\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_6h3\_ .node rect,#chatgpt-mermaid-\_r_6h3\_ .node circle,#chatgpt-mermaid-\_r_6h3\_ .node ellipse,#chatgpt-mermaid-\_r_6h3\_ .node polygon,#chatgpt-mermaid-\_r_6h3\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_6h3\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_6h3\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_6h3\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_6h3\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_6h3\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Client RequestExpress RouterControllerOperation Successful?Success Responsenext errorError MiddlewareError ResponseYesNo

Important: Express error-handling middleware is different from normal middleware. It has four parameters:

```
(err, req, res, next)
```

## 5. Syntax

### 5.1 JavaScript `try/catch`

```
try {

    // Code that may produce an error

} catch (error) {

    // Handle the error

}
```

### 5.2 Throw an error

```
throw new Error("Something went wrong");
```

### 5.3 Pass an error to Express

```
next(error);
```

### 5.4 Error-handling middleware

```
app.use((err, req, res, next) => {

    res.status(500).json({
        message: err.message
    });

});
```

### 5.5 Custom error

```
const error = new Error("Student not found");

error.statusCode = 404;

next(error);
```

### 5.6 Complete flow

```
Error Occurs
     ↓
Catch Error
     ↓
next(error)
     ↓
Error Middleware
     ↓
Send Error Response
```

## 6. Basic example

Let's understand JavaScript error handling first.

### Step 1: Create a JavaScript file

Create `error.js`.

```
// Try block
try {

    // This code produces an error
    console.log(student);

}

// Catch block
catch (error) {

    console.log("An error occurred");

    console.log(error.message);

}
```

### Step 2: Run the code

```
node error.js
```

### What happens?

1. JavaScript enters the `try` block.
2. It tries to access `student`.
3. `student` is not defined.
4. JavaScript creates a `ReferenceError`.
5. Execution moves to the `catch` block.
6. The error message is printed.

### Another example — Throw your own error

```
try {

    const age = 15;

    if (age < 18) {

        throw new Error("You are not eligible");

    }

    console.log("You are eligible");

}
catch (error) {

    console.log(error.message);

}
```

This example creates an error intentionally when the age is below 18.

## 7. Dry run

Let's execute the age example step by step.

```
const age = 15;

if (age < 18) {
    throw new Error("You are not eligible");
}
```

| Step | Execution           | Result               |
| ---- | ------------------- | -------------------- |
| 1    | `const age = 15`    | Age is 15            |
| 2    | `age < 18`          | `true`               |
| 3    | `throw new Error()` | Error is created     |
| 4    | `catch(error)`      | Error is caught      |
| 5    | `error.message`     | Message is displayed |

The important concept:

`throw` creates an error, and `catch` handles a synchronous error thrown inside the corresponding `try` block.

## 8. Output

### JavaScript example output

```
You are not eligible
```

### Express error example output

When an API sends an error response:

```
{
    "message": "Student not found"
}
```

HTTP status:

```
404 Not Found
```

## 9. Line-by-line explanation

Let's understand the following code.

```
try {

    const student = undefined;

    console.log(student.name);

}
catch (error) {

    console.log(error.message);

}
```

| Code            | Explanation                                       |
| --------------- | ------------------------------------------------- |
| `try`           | Starts a block of code where errors can be caught |
| `const student` | Creates a variable                                |
| `undefined`     | No object value is available                      |
| `student.name`  | Attempts to access a property                     |
| `catch(error)`  | Receives the thrown error                         |
| `error.message` | Reads the error message                           |

### Important error properties

JavaScript errors commonly provide:

| Property        | Purpose                   |
| --------------- | ------------------------- |
| `error.name`    | Error type                |
| `error.message` | Description of the error  |
| `error.stack`   | Stack trace for debugging |

Example:

```
try {

    throw new Error("Database failed");

}
catch (error) {

    console.log(error.name);

    console.log(error.message);

    console.log(error.stack);

}
```

Do not send full stack traces to normal API clients in production.

## 10. Practical example

Now let's learn the main Express error-handling concepts.

### 10.1 Types of errors

Errors can be grouped by where and why they happen.

| Error type           | Example                        |
| -------------------- | ------------------------------ |
| Validation error     | Missing student name           |
| Authentication error | Invalid token                  |
| Authorization error  | User lacks permission          |
| Not found error      | Student ID does not exist      |
| Database error       | Database connection fails      |
| Network error        | External API unavailable       |
| Server error         | Unexpected application problem |

### 10.2 Common HTTP error status codes

| Status | Name                  | When to use                           |
| ------ | --------------------- | ------------------------------------- |
| 400    | Bad Request           | Invalid input                         |
| 401    | Unauthorized          | Authentication is missing or invalid  |
| 403    | Forbidden             | User is authenticated but not allowed |
| 404    | Not Found             | Resource does not exist               |
| 409    | Conflict              | Resource conflicts with existing data |
| 422    | Unprocessable Content | Request data cannot be processed      |
| 429    | Too Many Requests     | Rate limit exceeded                   |
| 500    | Internal Server Error | Unexpected server error               |
| 502    | Bad Gateway           | Invalid upstream server response      |
| 503    | Service Unavailable   | Service temporarily unavailable       |
| 504    | Gateway Timeout       | Upstream server took too long         |

Remember the difference:

- `401`: Who are you? Authentication is required or invalid.
- `403`: I know who you are, but you are not allowed to do this.

### 10.3 Error handling using `try/catch`

Suppose you want to find a student.

```
app.get("/students/:id", (req, res) => {

    try {

        const id = Number(req.params.id);

        if (!Number.isInteger(id) || id <= 0) {

            throw new Error("Invalid student ID");

        }

        res.json({
            message: "Student ID is valid",
            id
        });

    }
    catch (error) {

        res.status(400).json({
            message: error.message
        });

    }

});
```

Test:

```
GET /students/abc
```

Response:

```
{
    "message": "Invalid student ID"
}
```

This is a basic example of handling a synchronous error inside a route.

### 10.4 Express error middleware

Instead of writing a `try/catch` and error response in every route, we can create one centralized error handler.

Example:

```
const express = require("express");

const app = express();

app.get("/error", (req, res, next) => {

    const error = new Error("Something went wrong");

    next(error);

});

// Centralized error middleware
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

Response:

```
{
    "message": "Something went wrong"
}
```

### 10.5 What is `next(error)`?

We already learned `next()` in Chapter 19.

There are two important uses:

```
next();
```

Moves to the next normal middleware or route handler.

```
next(error);
```

Passes an error to Express error-handling middleware.

Example:

```
app.get("/students", (req, res, next) => {

    try {

        throw new Error("Student data unavailable");

    }
    catch (error) {

        next(error);

    }

});
```

Express searches for the next error-handling middleware.

### 10.6 Custom errors

Sometimes JavaScript's normal `Error` object is not enough.

We want to attach an HTTP status code to the error.

We can create a custom error class.

Create `utils/AppError.js`

```
class AppError extends Error {

    constructor(message, statusCode) {

        // Pass message to the built-in Error class
        super(message);

        // Save HTTP status code
        this.statusCode = statusCode;

        // Identify expected application errors
        this.isOperational = true;

        // Capture stack trace
        Error.captureStackTrace(this, this.constructor);

    }

}

module.exports = AppError;
```

Now use it in a controller:

```
const AppError = require("../utils/AppError");

const getStudent = (req, res, next) => {

    const student = null;

    if (!student) {

        return next(
            new AppError("Student not found", 404)
        );

    }

    res.json(student);

};
```

The error contains:

```
message = "Student not found"
statusCode = 404
```

### 10.7 Centralized error handling

Create `middlewares/errorMiddleware.js`.

```
const errorMiddleware = (err, req, res, next) => {

    // Set default status code
    const statusCode = err.statusCode || 500;

    // Set default message
    const message = err.message || "Internal Server Error";

    // Log detailed error on the server
    console.error(err);

    // Send safe response to client
    res.status(statusCode).json({

        success: false,

        message: message

    });

};

module.exports = errorMiddleware;
```

Register it in `server.js`:

```
const express = require("express");

const app = express();

const errorMiddleware = require("./middlewares/errorMiddleware");

app.use(express.json());

app.get("/error", (req, res, next) => {

    const error = new Error("Something went wrong");

    error.statusCode = 500;

    next(error);

});

// Register error middleware after routes
app.use(errorMiddleware);

app.listen(3000);
```

### 10.8 Async error handling

In real applications, controllers often communicate with databases.

Database operations are asynchronous.

Example:

```
const getStudents = async (req, res, next) => {

    try {

        // Simulate an asynchronous database operation
        const students = await getStudentsFromDatabase();

        res.status(200).json({

            data: students

        });

    }
    catch (error) {

        next(error);

    }

};
```

The `try/catch` catches a rejected database operation and forwards the error.

Express version difference:

- Express 5: Rejected promises returned by async route handlers and middleware are automatically forwarded to error handling.
- Express 4: Use `try/catch` with `next(error)` or a compatible async wrapper.

For beginner learning, `try/catch` with `next(error)` is a clear approach that also works in Express 4 and Express 5.

### 10.9 Build a reusable async error handler

When many controllers use `try/catch`, we can create a reusable wrapper.

Create `utils/asyncHandler.js`:

```
const asyncHandler = (fn) => {

    return (req, res, next) => {

        Promise.resolve(fn(req, res, next))
            .catch(next);

    };

};

module.exports = asyncHandler;
```

Use it in your controller:

```
const asyncHandler = require("../utils/asyncHandler");

const getStudents = asyncHandler(async (req, res) => {

    const students = await getStudentsFromDatabase();

    res.status(200).json({

        data: students

    });

});

module.exports = {
    getStudents
};
```

How does it work?

1. `asyncHandler()` receives an async function.
2. The returned function executes that function.
3. `Promise.resolve()` handles its returned promise.
4. `.catch(next)` forwards a rejected promise to Express error middleware.

This wrapper is useful especially in Express 4. In Express 5, returned rejected promises are automatically forwarded, so this wrapper is usually unnecessary.

### 10.10 Complete reusable error-handling system

Let's combine the important concepts into one project.

Project structure

```
22_Express_Error_Handling/
│
├── controllers/
│   └── studentController.js
│
├── middlewares/
│   └── errorMiddleware.js
│
├── routes/
│   └── studentRoutes.js
│
├── utils/
│   ├── AppError.js
│   └── asyncHandler.js
│
├── server.js
│
├── package.json
│
└── .gitignore
```

1\. `utils/AppError.js`

```
class AppError extends Error {

    constructor(message, statusCode) {

        super(message);

        this.statusCode = statusCode;

        this.isOperational = true;

        Error.captureStackTrace(this, this.constructor);

    }

}

module.exports = AppError;
```

2\. `utils/asyncHandler.js`

```
const asyncHandler = (fn) => {

    return (req, res, next) => {

        Promise.resolve(fn(req, res, next))
            .catch(next);

    };

};

module.exports = asyncHandler;
```

3\. `controllers/studentController.js`

```
const AppError = require("../utils/AppError");

const asyncHandler = require("../utils/asyncHandler");

// Temporary student data
const students = [

    {
        id: 1,
        name: "Ramesh"
    },

    {
        id: 2,
        name: "Suresh"
    }

];

// GET ALL STUDENTS
const getStudents = asyncHandler(async (req, res) => {

    res.status(200).json({

        success: true,

        data: students

    });

});

// GET STUDENT BY ID
const getStudentById = asyncHandler(async (req, res, next) => {

    const id = Number(req.params.id);

    if (!Number.isInteger(id) || id <= 0) {

        return next(
            new AppError("Invalid student ID", 400)
        );

    }

    const student = students.find(
        (student) => student.id === id
    );

    if (!student) {

        return next(
            new AppError("Student not found", 404)
        );

    }

    res.status(200).json({

        success: true,

        data: student

    });

});

module.exports = {

    getStudents,

    getStudentById

};
```

4\. `routes/studentRoutes.js`

```
const express = require("express");

const router = express.Router();

const {

    getStudents,

    getStudentById

} = require("../controllers/studentController");

router.get("/", getStudents);

router.get("/:id", getStudentById);

module.exports = router;
```

5\. `middlewares/errorMiddleware.js`

```
const errorMiddleware = (err, req, res, next) => {

    const statusCode = err.statusCode || 500;

    const message = err.message || "Internal Server Error";

    // Log detailed error on the server
    console.error(err);

    res.status(statusCode).json({

        success: false,

        message: message

    });

};

module.exports = errorMiddleware;
```

6\. `server.js`

```
const express = require("express");

const app = express();

const studentRoutes = require("./routes/studentRoutes");

const errorMiddleware = require("./middlewares/errorMiddleware");

// Parse JSON
app.use(express.json());

// Register student routes
app.use("/api/students", studentRoutes);

// Handle unknown routes
app.use((req, res, next) => {

    const AppError = require("./utils/AppError");

    next(new AppError("Route not found", 404));

});

// Centralized error handler
app.use(errorMiddleware);

// Start server
app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

### Test in Postman

| Method | URL                 | Expected result        |
| ------ | ------------------- | ---------------------- |
| GET    | `/api/students`     | All students           |
| GET    | `/api/students/1`   | Student with ID 1      |
| GET    | `/api/students/99`  | 404 Student not found  |
| GET    | `/api/students/abc` | 400 Invalid student ID |
| GET    | `/unknown`          | 404 Route not found    |

Important: The example uses an in-memory array. Database errors will be handled in the same centralized way when we connect a real database.

## 11. Common mistakes

### Mistake 1 — Forgetting `next(error)`

Wrong:

```
catch (error) {

    console.log(error);

}
```

This logs the error but does not pass it to Express error middleware.

Correct:

```
catch (error) {

    next(error);

}
```

### Mistake 2 — Wrong error middleware parameters

Wrong:

```
app.use((req, res, next) => {

    res.status(500).send("Error");

});
```

This is normal middleware, not error-handling middleware.

Correct:

```
app.use((err, req, res, next) => {

    res.status(500).json({
        message: err.message
    });

});
```

### Mistake 3 — Registering error middleware before routes

Wrong:

```
app.use(errorMiddleware);

app.use("/api/students", studentRoutes);
```

Correct:

```
app.use("/api/students", studentRoutes);

app.use(errorMiddleware);
```

Error-handling middleware should generally be registered after the routes that may pass errors to it.

### Mistake 4 — Exposing sensitive error details

Wrong:

```
res.status(500).json({
    message: error.stack
});
```

Correct:

```
res.status(500).json({
    message: "Internal Server Error"
});
```

Log detailed errors on the server and return safe messages to clients.

### Mistake 5 — Forgetting `return`

Wrong:

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
```

### Mistake 6 — Assuming `try/catch` catches every asynchronous error

A `try/catch` catches errors from awaited operations inside its `try` block. It does not automatically catch errors from unrelated callbacks or detached asynchronous work.

Use proper Promise handling and Express error forwarding.

## 12. Best practices

1. Create a separate `errorMiddleware.js` file.
2. Use centralized error handling.
3. Create custom error classes when needed.
4. Use meaningful HTTP status codes.
5. Validate input before database operations.
6. Use `try/catch` appropriately for async operations.
7. Forward errors using `next(error)` when required.
8. Log detailed errors on the server.
9. Do not expose stack traces or secrets to clients.
10. Use a reusable async handler when useful.
11. Handle unknown routes.
12. Keep error responses consistent.

### Recommended error response structure

```
{
    "success": false,
    "message": "Student not found"
}
```

For validation errors, you might return additional details:

```
{
    "success": false,
    "message": "Validation failed",
    "errors": [
        "Name is required",
        "Email is required"
    ]
}
```

### GitHub README image folder

```
22_Express_Error_Handling/
│
├── images/
│   ├── error-flow.png
│   └── error-handling-architecture.png
│
└── README.md
```

Use actual files committed to your repository:

```
![Error Flow](./images/error-flow.png)

![Error Handling Architecture](./images/error-handling-architecture.png)
```

The Mermaid diagrams in this chapter can be pasted directly into GitHub README without creating image files.

## 13. Interview questions

### Beginner level

Q1. What is error handling in Express.js?

Error handling is the process of detecting errors and sending appropriate responses without exposing unnecessary internal details.

Q2. What is `try/catch`?

It is a JavaScript structure used to catch and handle errors thrown inside a `try` block.

Q3. What is `throw new Error()`?

It creates and throws a new JavaScript error.

Q4. What is `next(error)`?

It passes an error to Express error-handling middleware.

### Intermediate level

Q5. What is error-handling middleware?

It is Express middleware with four parameters:

```
(err, req, res, next)
```

Q6. What is a custom error class?

A class that extends JavaScript's `Error` class to add application-specific properties such as HTTP status codes.

Q7. What is centralized error handling?

Handling errors through one common middleware instead of writing separate error responses in every route.

Q8. What is the difference between 401 and 403?

- `401`: Authentication is missing or invalid.
- `403`: The user is authenticated but does not have permission.

### Advanced level

Q9. What is an async error handler?

A reusable function that handles rejected promises and forwards errors to Express error middleware.

Q10. How does Express 5 handle async errors?

Express 5 automatically forwards rejected promises returned by async route handlers and middleware to error-handling middleware.

Q11. Why should we not send `error.stack` to the client?

Because stack traces can expose internal implementation details, file paths, and sensitive information.

Q12. What is the purpose of custom error classes?

They provide consistent error messages and status codes for application-specific failures.

## 14. Practice problems

### Beginner exercises

1. Create a JavaScript `try/catch` example.
2. Throw an error if age is below 18.
3. Create an Express route that returns a 404 error.
4. Create an error middleware.
5. Test `next(error)` using Postman.

### Intermediate exercises

6. Create an `AppError` class.
7. Create centralized error middleware.
8. Handle missing student IDs.
9. Create a custom validation error.
10. Handle unknown routes.

### Advanced exercises

11. Build a reusable async error handler.
12. Create a Student API with centralized error handling.
13. Create consistent JSON error responses.
14. Handle database errors using error middleware.
15. Create a reusable error-handling system with custom errors and async controllers.

## 15. Mini challenge — Student API Error Handling

Your task

Build a Student Management API with a reusable error-handling system.

### Requirements

Create these endpoints:

```
GET     /api/students
GET     /api/students/:id
POST    /api/students
DELETE  /api/students/:id
```

### Expected behavior

| Situation               | Status |
| ----------------------- | ------ |
| Students fetched        | 200    |
| Student created         | 201    |
| Missing student         | 404    |
| Invalid ID              | 400    |
| Missing name            | 400    |
| Unknown route           | 404    |
| Unexpected server error | 500    |

### Expected project structure

```
22_Express_Error_Handling/
│
├── controllers/
│   └── studentController.js
│
├── routes/
│   └── studentRoutes.js
│
├── middlewares/
│   └── errorMiddleware.js
│
├── utils/
│   ├── AppError.js
│   └── asyncHandler.js
│
├── server.js
│
└── package.json
```

### Your task

Implement these functions:

1. `getStudents()`
2. `getStudentById()`
3. `createStudent()`
4. `deleteStudent()`
5. `errorMiddleware()`

Try to handle errors using `AppError` and centralized middleware.

## 16. Chapter summary

| Topic                | What you learned                             |
| -------------------- | -------------------------------------------- |
| Error handling       | Detecting and handling errors                |
| Error types          | Validation, authentication, database, server |
| `try/catch`          | Catches synchronous and awaited errors       |
| `throw`              | Creates and throws an error                  |
| `next(error)`        | Passes error to Express                      |
| Error middleware     | Handles application errors                   |
| Custom errors        | Adds application-specific error properties   |
| HTTP codes           | Communicates error types                     |
| Async errors         | Handles rejected promises                    |
| Async handler        | Reusable error-forwarding wrapper            |
| Centralized handling | Common error-handling system                 |

Main concept: Error handling makes your Express backend more reliable, secure, and easier to maintain.

## 17. Quick revision

🧠 Remember these important points

- `try/catch` handles errors.
- `throw` creates an error.
- `next(error)` forwards an error.
- Error middleware has four parameters.
- `AppError` creates custom application errors.
- `statusCode` stores the HTTP error status.
- Centralized middleware handles errors in one place.
- Express 5 automatically forwards rejected async handler promises.
- Never expose stack traces to clients.

  ⭐ Most important syntax

```
// Custom error
const error = new Error("Student not found");

error.statusCode = 404;

next(error);
```

```
// Error middleware
app.use((err, req, res, next) => {

    res.status(err.statusCode || 500).json({

        success: false,

        message: err.message

    });

});
```

Chapter 22 completed

Practice: Try the Student API Error Handling mini challenge.

When you're ready, type `NEXT` to start Chapter 23 — REST API Fundamentals, where we will learn REST, resources, endpoints, HTTP methods, CRUD, stateless architecture, JSON APIs, and REST conventions.