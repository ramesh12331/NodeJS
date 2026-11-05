# Chapter 20 — Express Router



PART 5 — EXPRESS.JS

Beginner to Advanced



## 🔑 Requires Before Starting

Before starting this chapter, you should understand:

1. Node.js: JavaScript runtime used to build backend applications.
2. Express.js: Framework used to create web servers and APIs.
3. Express routing: Handling HTTP requests using `GET`, `POST`, `PUT`, `PATCH`, and `DELETE`.
4. Middleware: Functions that execute during the request-response lifecycle.
5. Modules: Using `require()` and `module.exports` to share code between files.
6. HTTP methods: Different methods used to communicate with an API.

Example of a simple Express route:

```
app.get("/students", (req, res) => {
    res.json({
        message: "Student List"
    });
});
```

In this chapter, we will learn how to move routes into separate files and organize them professionally.

## 1. What is Express Router?

Express Router is a feature in Express.js that helps us create separate groups of routes and organize them into different files.

Without Express Router, we might write all routes inside one `server.js` file.

With Express Router, we can separate routes based on their purpose.

For example:

- Student routes
- Employee routes
- Product routes
- Customer routes
- Order routes

Express Router helps keep our backend application clean and manageable.

### Simple example

```
const express = require("express");

// Create a router
const router = express.Router();

// Create a route
router.get("/students", (req, res) => {

    res.send("Student List");

});

module.exports = router;
```

Here:

- `express.Router()` creates a router.
- `router.get()` creates a GET route.
- `module.exports` makes the router available to another file.

### 📖 Read

📖 Read — Understand Router

### 💡 Important

💡 Important — Remember

## 2. Why do we need Express Router?

Imagine building a Student Management API.

You have these routes:

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

GET     /courses
POST    /courses
GET     /courses/:id
PUT     /courses/:id
DELETE  /courses/:id
```

If you write all these routes in one file, `server.js` becomes very large.

### Without Express Router

```
project/
│
└── server.js
    ├── Student routes
    ├── Teacher routes
    ├── Course routes
    ├── Employee routes
    └── Product routes
```

Problems:

1. Large files.
2. Difficult to understand.
3. Difficult to maintain.
4. Difficult to debug.
5. Difficult for multiple developers to work together.

### With Express Router

```
project/
│
├── routes/
│   ├── studentRoutes.js
│   ├── teacherRoutes.js
│   ├── courseRoutes.js
│   ├── employeeRoutes.js
│   └── productRoutes.js
│
└── server.js
```

Now each file manages its own routes.

Main purpose: Express Router helps us separate routes into reusable and manageable modules.

## 3. Real-world analogy

[Central Square](https://images.openai.com/static-rsc-4/8c1dHMflsf2XrQQ0b2Fn9jG9xmBt-2UBAg9JAmCrJAQAPxNrkzSN-rvlJ0o5LQwk8zWRNYJ2-ThiHuYFMMJuiePr0CLAGv5DTkkguJwym5_pLwDFEZPEid-4jzTBKfdG1jsrJufaHIHVLcnwW4HHDs6ke193kIOWGX-LbzP8RlU?purpose=inline)

[centralsq.co.uk](https://www.centralsq.co.uk/?utm_source=chatgpt.com)

Imagine an office building with different departments.

| Office department  | Express Router           |
| ------------------ | ------------------------ |
| HR department      | Employee router          |
| Finance department | Payment router           |
| Sales department   | Product router           |
| Student department | Student router           |
| Main reception     | Main Express application |

The main application connects all the routers, just like a reception connects visitors to different departments.

## 4. Architecture / Flow

### How Express Router works

Client Request

GET /api/students

server.js

Main Express application

app.use("/api/students", studentRoutes)

Mount the student router

studentRoutes.js

router.get("/")

Response

Student list in JSON

### GitHub Mermaid diagram

You can copy this directly into your `README.md`.

\#chatgpt-mermaid-\_r_5n2\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_5n2\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_5n2\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_5n2\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_5n2\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5n2\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_5n2\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_5n2\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_5n2\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_5n2\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_5n2\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_5n2\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_5n2\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_5n2\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_5n2\_ p{margin:0;}#chatgpt-mermaid-\_r_5n2\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5n2\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5n2\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5n2\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_5n2\_ .label text,#chatgpt-mermaid-\_r_5n2\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5n2\_ .node rect,#chatgpt-mermaid-\_r_5n2\_ .node circle,#chatgpt-mermaid-\_r_5n2\_ .node ellipse,#chatgpt-mermaid-\_r_5n2\_ .node polygon,#chatgpt-mermaid-\_r_5n2\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_5n2\_ .rough-node .label text,#chatgpt-mermaid-\_r_5n2\_ .node .label text,#chatgpt-mermaid-\_r_5n2\_ .image-shape .label,#chatgpt-mermaid-\_r_5n2\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_5n2\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_5n2\_ .rough-node .label,#chatgpt-mermaid-\_r_5n2\_ .node .label,#chatgpt-mermaid-\_r_5n2\_ .image-shape .label,#chatgpt-mermaid-\_r_5n2\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_5n2\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_5n2\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_5n2\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_5n2\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_5n2\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_5n2\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_5n2\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_5n2\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_5n2\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_5n2\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_5n2\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5n2\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5n2\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_5n2\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5n2\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_5n2\_ .icon-shape,#chatgpt-mermaid-\_r_5n2\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_5n2\_ .icon-shape p,#chatgpt-mermaid-\_r_5n2\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_5n2\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_5n2\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_5n2\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_5n2\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_5n2\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_5n2\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_5n2\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_5n2\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_5n2\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_5n2\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_5n2\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_5n2\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_5n2\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_5n2\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_5n2\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_5n2\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_5n2\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_5n2\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_5n2\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_5n2\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_5n2\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_5n2\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_5n2\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_5n2\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_5n2\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_5n2\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_5n2\_ .node rect,#chatgpt-mermaid-\_r_5n2\_ .node circle,#chatgpt-mermaid-\_r_5n2\_ .node ellipse,#chatgpt-mermaid-\_r_5n2\_ .node polygon,#chatgpt-mermaid-\_r_5n2\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_5n2\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_5n2\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_5n2\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_5n2\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_5n2\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Client Requestserver.jsMount Student RouterstudentRoutes.jsRoute HandlerResponse to ClientMount Employee RouteremployeeRoutes.jsEmployee Route Handler

### Understand URL mapping

Suppose your `server.js` contains:

```
app.use("/api/students", studentRoutes);
```

And `studentRoutes.js` contains:

```
router.get("/", (req, res) => {
    res.send("Student List");
});
```

The final URL becomes:

```
/api/students + /
      ↓
/api/students/
```

Another example:

```
router.get("/:id", (req, res) => {
    res.send("Student Details");
});
```

Final URL:

```
/api/students/:id
```

Example request:

```
GET /api/students/101
```

Important: The prefix in `app.use()` is combined with the route path inside the router.

## 5. Syntax

### Step 1: Import Express

```
const express = require("express");
```

### Step 2: Create a router

```
const router = express.Router();
```

### Step 3: Create routes

```
router.get("/", (req, res) => {
    res.send("Get Students");
});

router.post("/", (req, res) => {
    res.send("Create Student");
});
```

### Step 4: Export router

```
module.exports = router;
```

### Step 5: Import router into server.js

```
const studentRoutes = require("./routes/studentRoutes");
```

### Step 6: Register router

```
app.use("/api/students", studentRoutes);
```

### Complete syntax flow

```
Create Router
     ↓
Create Routes
     ↓
Export Router
     ↓
Import Router
     ↓
Register with app.use()
     ↓
Access API
```

## 6. Basic example

Let's create our first Express Router project.

### Project structure

```
20_Express_Router/
│
├── node_modules/
│
├── routes/
│   └── studentRoutes.js
│
├── server.js
│
└── package.json
```

### Step 1: Create project

```
mkdir 20_Express_Router

cd 20_Express_Router

npm init -y

npm install express
```

### Step 2: Create `routes/studentRoutes.js`

```
const express = require("express");

// Create a router
const router = express.Router();

// GET - Student list
router.get("/", (req, res) => {

    res.json({
        message: "Student List"
    });

});

// GET - Single student
router.get("/:id", (req, res) => {

    const studentId = req.params.id;

    res.json({
        message: "Student Details",
        id: studentId
    });

});

// POST - Create student
router.post("/", (req, res) => {

    res.json({
        message: "Student Created"
    });

});

// Export router
module.exports = router;
```

### Step 3: Create `server.js`

```
const express = require("express");

const app = express();

// Parse JSON request body
app.use(express.json());

// Import student router
const studentRoutes = require("./routes/studentRoutes");

// Register student router
app.use("/api/students", studentRoutes);

// Start server
app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

### Step 4: Start server

```
node server.js
```

### Step 5: Test APIs in Postman

| Method | URL                                      |
| ------ | ---------------------------------------- |
| GET    | `http://localhost:3000/api/students`     |
| GET    | `http://localhost:3000/api/students/101` |
| POST   | `http://localhost:3000/api/students`     |

For POST, send JSON:

```
{
    "name": "Ramesh",
    "email": "ramesh@example.com"
}
```

## 7. Dry run

Let's understand this request:

```
GET http://localhost:3000/api/students/101
```

### Step-by-step execution

Step 1: Client sends request.

```
/api/students/101
```

Step 2: Express checks the registered router.

```
app.use("/api/students", studentRoutes);
```

The matching prefix is:

```
/api/students
```

Step 3: Express passes the remaining path to the student router.

```
/101
```

Step 4: Express matches this route:

```
router.get("/:id", (req, res) => {
```

Step 5: Express extracts the route parameter.

```
const studentId = req.params.id;
```

Value:

```
studentId = "101"
```

Step 6: Sends response.

```
res.json({
    message: "Student Details",
    id: studentId
});
```

## 8. Output

### Terminal

```
Server running on port 3000
```

### GET `/api/students`

```
{
    "message": "Student List"
}
```

### GET `/api/students/101`

```
{
    "message": "Student Details",
    "id": "101"
}
```

### POST `/api/students`

```
{
    "message": "Student Created"
}
```

## 9. Line-by-line explanation

Let's understand the most important lines.

```
const express = require("express");
```

Imports the Express package.

```
const router = express.Router();
```

Creates a new router object.

```
router.get("/", (req, res) => {
```

Creates a GET route on the router.

```
router.get("/:id", (req, res) => {
```

Creates a route with a dynamic parameter.

```
const studentId = req.params.id;
```

Reads the ID from the URL.

```
module.exports = router;
```

Exports the router so another file can import it.

In `server.js`:

```
const studentRoutes = require("./routes/studentRoutes");
```

Imports the exported router.

```
app.use("/api/students", studentRoutes);
```

Connects the router to the main Express application using the `/api/students` prefix.

### Important difference

| `app`                                  | `router`                        |
| -------------------------------------- | ------------------------------- |
| Main Express application               | Separate route group            |
| Created with `express()`               | Created with `express.Router()` |
| Uses `app.get()`                       | Uses `router.get()`             |
| Uses `app.use()`                       | Uses `router.use()`             |
| Starts the server using `app.listen()` | Does not start a server         |

## 10. Practical example

Now let's build a more professional Student Management API using separate route files.

### 10.1 Route separation

Suppose your application has students and employees.

We can create:

```
routes/
│
├── studentRoutes.js
└── employeeRoutes.js
```

studentRoutes.js

```
const express = require("express");

const router = express.Router();

router.get("/", (req, res) => {

    res.json({
        message: "All Students"
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

employeeRoutes.js

```
const express = require("express");

const router = express.Router();

router.get("/", (req, res) => {

    res.json({
        message: "All Employees"
    });

});

router.get("/:id", (req, res) => {

    res.json({
        message: "Employee Details",
        id: req.params.id
    });

});

module.exports = router;
```

server.js

```
const express = require("express");

const app = express();

app.use(express.json());

// Import routers
const studentRoutes = require("./routes/studentRoutes");
const employeeRoutes = require("./routes/employeeRoutes");

// Register routers
app.use("/api/students", studentRoutes);
app.use("/api/employees", employeeRoutes);

app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Now the URLs are:

```
GET /api/students
GET /api/students/101

GET /api/employees
GET /api/employees/201
```

### 10.2 Modular routes

Modular routes means splitting route definitions into separate files based on features or resources.

For example:

```
routes/
│
├── authRoutes.js
├── userRoutes.js
├── productRoutes.js
├── orderRoutes.js
└── paymentRoutes.js
```

Each router manages its own resource.

This is especially useful in large applications.

### 10.3 Route files

A route file defines:

- URL paths.
- HTTP methods.
- Route-specific middleware.
- The controller function that handles the request.

Example:

```
const express = require("express");

const router = express.Router();

// Route definition
router.get("/", (req, res) => {

    res.json({
        message: "Products"
    });

});

module.exports = router;
```

For now, we are writing the response inside the route. In the next chapter, we will move business logic into separate controller files.

### 10.4 Professional folder structure

As your backend grows, you should organize your application like this:

```
backend/
│
├── config/
│   └── db.js
│
├── controllers/
│   ├── studentController.js
│   └── employeeController.js
│
├── models/
│   ├── Student.js
│   └── Employee.js
│
├── routes/
│   ├── studentRoutes.js
│   └── employeeRoutes.js
│
├── middlewares/
│   ├── authMiddleware.js
│   └── errorMiddleware.js
│
├── services/
│   └── studentService.js
│
├── utils/
│   └── response.js
│
├── .env
├── .gitignore
├── package.json
└── server.js
```

Let's understand each folder:

| Folder         | Responsibility                         |
| -------------- | -------------------------------------- |
| `config/`      | Database and application configuration |
| `controllers/` | Handles request and response logic     |
| `models/`      | Database models and schemas            |
| `routes/`      | API endpoint definitions               |
| `middlewares/` | Authentication, validation, logging    |
| `services/`    | Business logic and reusable operations |
| `utils/`       | Helper functions                       |

### 10.5 How files connect

\#chatgpt-mermaid-\_r_5ud\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_5ud\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_5ud\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_5ud\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_5ud\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5ud\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_5ud\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_5ud\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_5ud\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_5ud\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_5ud\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_5ud\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_5ud\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_5ud\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_5ud\_ p{margin:0;}#chatgpt-mermaid-\_r_5ud\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5ud\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5ud\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5ud\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_5ud\_ .label text,#chatgpt-mermaid-\_r_5ud\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5ud\_ .node rect,#chatgpt-mermaid-\_r_5ud\_ .node circle,#chatgpt-mermaid-\_r_5ud\_ .node ellipse,#chatgpt-mermaid-\_r_5ud\_ .node polygon,#chatgpt-mermaid-\_r_5ud\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_5ud\_ .rough-node .label text,#chatgpt-mermaid-\_r_5ud\_ .node .label text,#chatgpt-mermaid-\_r_5ud\_ .image-shape .label,#chatgpt-mermaid-\_r_5ud\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_5ud\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_5ud\_ .rough-node .label,#chatgpt-mermaid-\_r_5ud\_ .node .label,#chatgpt-mermaid-\_r_5ud\_ .image-shape .label,#chatgpt-mermaid-\_r_5ud\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_5ud\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_5ud\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_5ud\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_5ud\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_5ud\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_5ud\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_5ud\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_5ud\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_5ud\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_5ud\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_5ud\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5ud\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5ud\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_5ud\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_5ud\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_5ud\_ .icon-shape,#chatgpt-mermaid-\_r_5ud\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_5ud\_ .icon-shape p,#chatgpt-mermaid-\_r_5ud\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_5ud\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_5ud\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_5ud\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_5ud\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_5ud\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_5ud\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_5ud\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_5ud\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_5ud\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_5ud\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_5ud\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_5ud\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_5ud\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_5ud\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_5ud\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_5ud\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_5ud\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_5ud\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_5ud\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_5ud\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_5ud\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_5ud\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_5ud\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_5ud\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_5ud\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_5ud\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_5ud\_ .node rect,#chatgpt-mermaid-\_r_5ud\_ .node circle,#chatgpt-mermaid-\_r_5ud\_ .node ellipse,#chatgpt-mermaid-\_r_5ud\_ .node polygon,#chatgpt-mermaid-\_r_5ud\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_5ud\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_5ud\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_5ud\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_5ud\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_5ud\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Clientserver.jsroutesmiddlewarescontrollersservicesmodelsDatabaseResponse

This is a common way to organize a backend application. The exact architecture can vary depending on project size and requirements.

### 10.6 Why separate routes and controllers?

Imagine your Student API has 30 routes.

If you put every route and all business logic into one file, it becomes difficult to manage.

Instead:

- Route files define which URL calls which function.
- Controller files handle request and response logic.
- Model files represent database data.

We will study controllers in detail in Chapter 21.

## 11. Common mistakes

### Mistake 1 — Forgetting to export the router

Wrong:

```
const router = express.Router();

router.get("/", (req, res) => {
    res.send("Students");
});

// Forgot module.exports
```

Correct:

```
module.exports = router;
```

### Mistake 2 — Wrong import path

Wrong:

```
const studentRoutes = require("./studentRoutes");
```

If your file is inside the `routes` folder, this path is incorrect.

Correct:

```
const studentRoutes = require("./routes/studentRoutes");
```

### Mistake 3 — Forgetting to register the router

Wrong:

```
const studentRoutes = require("./routes/studentRoutes");

// Router imported but not registered
```

Correct:

```
app.use("/api/students", studentRoutes);
```

### Mistake 4 — Confusing the route path

Suppose:

```
app.use("/api/students", studentRoutes);
```

Inside `studentRoutes.js`:

```
router.get("/", (req, res) => {
    res.send("Students");
});
```

Correct URL:

```
/api/students
```

Not:

```
/students
```

### Mistake 5 — Using `app.get()` instead of `router.get()`

Inside a router file, use:

```
router.get("/", (req, res) => {
    res.send("Students");
});
```

The router file should define routes on its router object.

## 12. Best practices

1. Create separate router files for different resources.
2. Use meaningful filenames such as `studentRoutes.js`.
3. Keep `server.js` clean.
4. Use a common API prefix such as `/api`.
5. Keep routes focused on URL and HTTP method definitions.
6. Use middleware where required.
7. Export routers correctly.
8. Use controllers to separate request-handling logic.
9. Use consistent URL naming conventions.
10. Avoid creating unnecessary files for very small applications.

### Professional URL naming

Prefer plural resource names:

```
/api/students
/api/employees
/api/products
/api/orders
```

Use route parameters for individual resources:

```
/api/students/101
/api/products/501
```

## 13. Interview questions

### Beginner level

Q1. What is Express Router?

Express Router is a feature that helps organize routes into separate modules.

Q2. How do you create a router?

```
const router = express.Router();
```

Q3. How do you export a router?

```
module.exports = router;
```

Q4. How do you connect a router to the main application?

```
app.use("/api/students", studentRoutes);
```

### Intermediate level

Q5. What is the difference between `app` and `router`?

`app` represents the main Express application. `router` represents a separate group of routes.

Q6. Why do we use separate route files?

To organize code, improve maintainability, reduce duplication, and make applications easier to understand.

Q7. What is modular routing?

Modular routing means separating route definitions into multiple files based on application features or resources.

Q8. Can we use middleware inside Express Router?

Yes. We can use `router.use()` for router-level middleware or pass middleware directly to a route.

### Advanced level

Q9. What happens when we use `app.use("/api/students", studentRoutes)`?

Express mounts the student router at `/api/students`. Requests matching this prefix can be handled by routes defined inside that router.

Q10. Can we create multiple routers in one application?

Yes. We can create separate routers for students, employees, products, customers, and other resources.

Q11. What is the benefit of route separation in large applications?

It improves maintainability, code reuse, testing, collaboration, and scalability.

Q12. Can we apply middleware to a specific router?

Yes:

```
router.use(authMiddleware);
```

This applies the middleware to requests handled by that router, subject to its route and mount path.

## 14. Practice problems

### Beginner exercises

1. Create a router for students.
2. Create a router for employees.
3. Create a GET route inside each router.
4. Export both routers.
5. Import both routers into `server.js`.

### Intermediate exercises

6. Create a Product Router with GET and POST routes.
7. Create a Customer Router with GET, POST, PUT and DELETE routes.
8. Add route parameters to student routes.
9. Add middleware to the employee router.
10. Create separate route files for books and authors.

### Advanced exercises

11. Build a complete Student Management API using separate route files.
12. Create five routers: users, products, orders, customers and payments.
13. Apply authentication middleware only to protected routers.
14. Organize a backend using `routes/`, `controllers/`, `models/`, `middlewares/`, `services/`, and `utils/`.
15. Build a modular API with consistent `/api` prefixes.

## 15. Mini challenge — Student and Employee Router

Your task

Build an application with two independent routers.

### Requirements

Student routes

```
GET     /api/students
POST    /api/students
GET     /api/students/:id
```

Employee routes

```
GET     /api/employees
POST    /api/employees
GET     /api/employees/:id
```

### Expected project structure

```
20_Express_Router/
│
├── routes/
│   ├── studentRoutes.js
│   └── employeeRoutes.js
│
├── server.js
│
└── package.json
```

### Expected responses

GET `/api/students`

```
{
    "message": "All Students"
}
```

GET `/api/employees/201`

```
{
    "message": "Employee Details",
    "id": "201"
}
```

### Your task

Try creating both routers without copying the complete example above.

Think about these steps:

1. Create the student router.
2. Create the employee router.
3. Export both routers.
4. Import both into `server.js`.
5. Register them with `app.use()`.
6. Test all routes using Postman.

## 16. Chapter summary

| Topic              | What you learned                       |
| ------------------ | -------------------------------------- |
| Express Router     | Organizes routes into separate modules |
| `express.Router()` | Creates a router                       |
| `router.get()`     | Creates a GET route                    |
| `router.post()`    | Creates a POST route                   |
| `module.exports`   | Exports the router                     |
| `require()`        | Imports the router                     |
| `app.use()`        | Mounts the router                      |
| Route separation   | Moves routes into separate files       |
| Modular routing    | Organizes routes by resource           |
| Project structure  | Separates backend responsibilities     |

Main concept: Express Router helps you build clean, modular, and maintainable backend applications.

## 17. Quick revision

🧠 Remember these important points

- `express()` creates the main Express application.
- `express.Router()` creates a separate router.
- `router.get()` creates a GET route.
- `router.post()` creates a POST route.
- `module.exports` exports the router.
- `require()` imports the router.
- `app.use()` connects the router to the application.
- Route prefixes are combined with router paths.
- Separate route files make projects easier to maintain.

  ⭐ Most important syntax

```
// studentRoutes.js

const express = require("express");

const router = express.Router();

router.get("/", (req, res) => {

    res.json({
        message: "Student List"
    });

});

module.exports = router;
```

```
// server.js

const express = require("express");

const app = express();

const studentRoutes = require("./routes/studentRoutes");

app.use("/api/students", studentRoutes);

app.listen(3000);
```

Chapter 20 completed

Practice: Complete the Student and Employee Router mini challenge.

When you're ready, type `NEXT` to start Chapter 21 — Controllers, where we will learn how to separate route definitions from request-handling logic.