# Chapter 21 — Express Controllers



PART 5 — EXPRESS.JS

Beginner to Advanced



## 🔑 Requires Before Starting

Before learning controllers, you should understand:

1. Node.js: JavaScript runtime used for backend development.
2. Express.js: Framework used to build APIs and web servers.
3. Express routing: Handling HTTP requests using `GET`, `POST`, `PUT`, `PATCH`, and `DELETE`.
4. Express Router: Separating routes into different files using `express.Router()`.
5. Middleware: Functions that execute between a request and response.
6. Modules: Using `require()` and `module.exports` to share code between files.
7. Request and response: Understanding `req` and `res`.

You already learned how to create separate route files in Chapter 20. Now we will learn how to separate the actual logic from those route files.

## 1. What is a Controller?

A controller is a function that handles an incoming request and sends an appropriate response to the client.

It generally contains request-handling logic.

For example, consider a Student Management API.

You need to:

- Get all students.
- Get one student.
- Create a student.
- Update a student.
- Delete a student.

Instead of writing all this logic inside route files, we create a separate controller file.

### Without controllers

```
const express = require("express");

const router = express.Router();

router.get("/students", (req, res) => {

    // Request handling logic
    // Business operations
    // Response handling

    res.json({
        message: "Student List"
    });

});

module.exports = router;
```

### With controllers

studentRoutes.js

```
router.get("/students", getStudents);
```

studentController.js

```
const getStudents = (req, res) => {

    res.json({
        message: "Student List"
    });

};
```

Now routes and request-handling logic are separated.

### 📖 Read

📖 Read — Understand Controllers

### 💡 Important

💡 Important — Remember

## 2. Why do we need Controllers?

Imagine you are building a large Student Management API.

You have 30 routes.

If you write all request-handling logic inside route files, those files become very large.

### Without controllers

```
backend/
│
├── routes/
│   └── studentRoutes.js
│       ├── Get students logic
│       ├── Get student by ID logic
│       ├── Create student logic
│       ├── Update student logic
│       └── Delete student logic
│
└── server.js
```

Problems:

1. Route files become large.
2. Difficult to understand.
3. Difficult to maintain.
4. Difficult to test.
5. Difficult to reuse logic.

### With controllers

```
backend/
│
├── routes/
│   └── studentRoutes.js
│
├── controllers/
│   └── studentController.js
│
└── server.js
```

Now:

- Routes define API endpoints.
- Controllers handle incoming requests and outgoing responses.

### Benefits

- Clean code.
- Better organization.
- Easier debugging.
- Easier testing.
- Easier teamwork.
- Better maintainability.

## 3. Real-world analogy

[Smart Order | Restaurant ticketing, kitchen, and admin dashboards](https://images.openai.com/static-rsc-4/BzUi_dIROKbt_jjo03tE9MRgN71SZwHvRoDfoc0IQHxfzjfx-_fHztdN7SwEocro4hazUyPiEJ5cHQ1YHJW9ja5iM5FcScb-i_77BbP_KyYzkajlS7ps4qCuR5xTwBXj9XTM8iB6FMJGXfIewUfa9bXJjVA5wDkXNfaXYqqiqjY?purpose=inline)

[order.elyx.work](https://order.elyx.work/?utm_source=chatgpt.com)

Imagine ordering food in a restaurant.

| Restaurant              | Express application          |
| ----------------------- | ---------------------------- |
| Customer                | Client                       |
| Waiter receives order   | Route                        |
| Kitchen prepares food   | Controller                   |
| Ingredients and recipes | Data and business operations |
| Waiter serves food      | Response                     |

Example:

1. Customer requests a pizza.
2. Waiter receives the order.
3. Kitchen prepares the pizza.
4. Waiter serves the pizza.

Similarly:

1. Client sends a GET request.
2. Express route receives the request.
3. Controller processes it.
4. Controller sends a response.

## 4. Architecture / Flow

### Controller request lifecycle

Client

Browser / Postman / React

Route

studentRoutes.js

Controller

studentController.js

Data / Business Operations

Process request and work with data

Response

JSON sent to client

### GitHub Mermaid diagram

Copy this diagram into your `README.md`.

\#chatgpt-mermaid-\_r_65f\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_65f\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_65f\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_65f\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_65f\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_65f\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_65f\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_65f\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_65f\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_65f\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_65f\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_65f\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_65f\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_65f\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_65f\_ p{margin:0;}#chatgpt-mermaid-\_r_65f\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_65f\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_65f\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_65f\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_65f\_ .label text,#chatgpt-mermaid-\_r_65f\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_65f\_ .node rect,#chatgpt-mermaid-\_r_65f\_ .node circle,#chatgpt-mermaid-\_r_65f\_ .node ellipse,#chatgpt-mermaid-\_r_65f\_ .node polygon,#chatgpt-mermaid-\_r_65f\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_65f\_ .rough-node .label text,#chatgpt-mermaid-\_r_65f\_ .node .label text,#chatgpt-mermaid-\_r_65f\_ .image-shape .label,#chatgpt-mermaid-\_r_65f\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_65f\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_65f\_ .rough-node .label,#chatgpt-mermaid-\_r_65f\_ .node .label,#chatgpt-mermaid-\_r_65f\_ .image-shape .label,#chatgpt-mermaid-\_r_65f\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_65f\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_65f\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_65f\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_65f\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_65f\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_65f\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_65f\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_65f\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_65f\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_65f\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_65f\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_65f\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_65f\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_65f\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_65f\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_65f\_ .icon-shape,#chatgpt-mermaid-\_r_65f\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_65f\_ .icon-shape p,#chatgpt-mermaid-\_r_65f\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_65f\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_65f\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_65f\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_65f\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_65f\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_65f\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_65f\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_65f\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_65f\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_65f\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_65f\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_65f\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_65f\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_65f\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_65f\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_65f\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_65f\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_65f\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_65f\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_65f\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_65f\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_65f\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_65f\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_65f\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_65f\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_65f\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_65f\_ .node rect,#chatgpt-mermaid-\_r_65f\_ .node circle,#chatgpt-mermaid-\_r_65f\_ .node ellipse,#chatgpt-mermaid-\_r_65f\_ .node polygon,#chatgpt-mermaid-\_r_65f\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_65f\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_65f\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_65f\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_65f\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_65f\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Client RequestExpress RouterStudent ControllerProcess RequestRead or Update DataSend JSON Response

### Understand the connection

Route file:

```
router.get("/", getStudents);
```

Controller file:

```
const getStudents = (req, res) => {

    res.json({
        message: "Student List"
    });

};
```

The route calls the controller when a matching request arrives.

## 5. Syntax

### Controller function syntax

```
const functionName = (req, res) => {

    // Handle incoming request

    // Perform operations

    // Send response

};
```

### Export controller

```
module.exports = {
    functionName
};
```

### Import controller

```
const {
    functionName
} = require("../controllers/studentController");
```

### Connect controller to route

```
router.get("/", functionName);
```

### Complete flow

```
Create Controller Function
          ↓
Export Controller
          ↓
Import into Route File
          ↓
Connect to HTTP Method
          ↓
Client Sends Request
          ↓
Controller Executes
          ↓
Response Sent
```

## 6. Basic example

Let's create a simple Student API using controllers.

### Project structure

```
21_Express_Controllers/
│
├── controllers/
│   └── studentController.js
│
├── routes/
│   └── studentRoutes.js
│
├── server.js
│
└── package.json
```

### Step 1: Install Express

```
npm init -y

npm install express
```

### Step 2: Create `controllers/studentController.js`

```
// Get all students
const getStudents = (req, res) => {

    res.json({
        message: "All Students"
    });

};

// Export controller functions
module.exports = {
    getStudents
};
```

### Step 3: Create `routes/studentRoutes.js`

```
const express = require("express");

const router = express.Router();

// Import controller
const {
    getStudents
} = require("../controllers/studentController");

// Connect route with controller
router.get("/", getStudents);

module.exports = router;
```

### Step 4: Create `server.js`

```
const express = require("express");

const app = express();

// Import student routes
const studentRoutes = require("./routes/studentRoutes");

// Register router
app.use("/api/students", studentRoutes);

// Start server
app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

### Step 5: Run the server

```
node server.js
```

Test:

```
GET http://localhost:3000/api/students
```

## 7. Dry run

Let's understand how the request works.

Request:

```
GET /api/students
```

### Step-by-step execution

Step 1: Client sends a request.

```
GET /api/students
```

Step 2: Express checks `server.js`.

```
app.use("/api/students", studentRoutes);
```

Step 3: Express enters `studentRoutes.js`.

```
router.get("/", getStudents);
```

Step 4: Express calls the controller.

```
const getStudents = (req, res) => {
```

Step 5: Controller sends a response.

```
res.json({
    message: "All Students"
});
```

Step 6: Client receives the response.

```
Request → Route → Controller → Response
```

## 8. Output

### Terminal

```
Server running on port 3000
```

### Postman response

```
{
    "message": "All Students"
}
```

### HTTP status

```
200 OK
```

## 9. Line-by-line explanation

Let's understand the important code.

### Controller file

```
const getStudents = (req, res) => {

    res.json({
        message: "All Students"
    });

};
```

| Code                | Explanation                    |
| ------------------- | ------------------------------ |
| `const getStudents` | Creates a controller function  |
| `req`               | Contains incoming request data |
| `res`               | Used to send the response      |
| `res.json()`        | Sends a JSON response          |
| `message`           | Response data                  |

### Export

```
module.exports = {
    getStudents
};
```

This makes the controller available to other files.

### Route file

```
const {
    getStudents
} = require("../controllers/studentController");
```

This imports the controller function.

```
router.get("/", getStudents);
```

This connects the GET route to the controller.

### Why not write this?

```
router.get("/", (req, res) => {

    res.json({
        message: "All Students"
    });

});
```

We can write this for small applications. However, for larger applications, separating the controller makes the code easier to manage.

## 10. Practical example

Now let's build a complete Student Management CRUD API using controllers.

We will use an array for storage so you can understand the controller logic before learning database operations.

### 10.1 Project structure

```
21_Express_Controllers/
│
├── controllers/
│   └── studentController.js
│
├── routes/
│   └── studentRoutes.js
│
├── server.js
│
├── package.json
│
└── .gitignore
```

### 10.2 Create `controllers/studentController.js`

```
// Temporary student data
let students = [

    {
        id: 1,
        name: "Ramesh",
        email: "ramesh@example.com"
    },

    {
        id: 2,
        name: "Suresh",
        email: "suresh@example.com"
    }

];

// ==================================
// GET ALL STUDENTS
// ==================================

const getStudents = (req, res) => {

    res.status(200).json({

        message: "Students fetched successfully",

        data: students

    });

};


// ==================================
// GET SINGLE STUDENT
// ==================================

const getStudentById = (req, res) => {

    // Read ID from URL
    const id = Number(req.params.id);

    // Find student
    const student = students.find(
        (student) => student.id === id
    );

    // Check student exists
    if (!student) {

        return res.status(404).json({

            message: "Student not found"

        });

    }

    // Send response
    res.status(200).json({

        message: "Student fetched successfully",

        data: student

    });

};


// ==================================
// CREATE STUDENT
// ==================================

const createStudent = (req, res) => {

    // Read data from request body
    const { name, email } = req.body;

    // Validate required fields
    if (!name || !email) {

        return res.status(400).json({

            message: "Name and email are required"

        });

    }

    // Create new student
    const newStudent = {

        id: students.length
            ? Math.max(...students.map(student => student.id)) + 1
            : 1,

        name,

        email

    };

    // Store student
    students.push(newStudent);

    // Send response
    res.status(201).json({

        message: "Student created successfully",

        data: newStudent

    });

};


// ==================================
// UPDATE STUDENT
// ==================================

const updateStudent = (req, res) => {

    // Read ID
    const id = Number(req.params.id);

    // Find student
    const student = students.find(
        (student) => student.id === id
    );

    // Check student exists
    if (!student) {

        return res.status(404).json({

            message: "Student not found"

        });

    }

    // Update provided fields
    const { name, email } = req.body;

    if (name !== undefined) {
        student.name = name;
    }

    if (email !== undefined) {
        student.email = email;
    }

    // Send response
    res.status(200).json({

        message: "Student updated successfully",

        data: student

    });

};


// ==================================
// DELETE STUDENT
// ==================================

const deleteStudent = (req, res) => {

    // Read ID
    const id = Number(req.params.id);

    // Find student index
    const studentIndex = students.findIndex(
        (student) => student.id === id
    );

    // Check student exists
    if (studentIndex === -1) {

        return res.status(404).json({

            message: "Student not found"

        });

    }

    // Remove student
    const deletedStudent = students.splice(
        studentIndex,
        1
    )[0];

    // Send response
    res.status(200).json({

        message: "Student deleted successfully",

        data: deletedStudent

    });

};


// Export all controller functions
module.exports = {

    getStudents,

    getStudentById,

    createStudent,

    updateStudent,

    deleteStudent

};
```

### 10.3 Create `routes/studentRoutes.js`

```
const express = require("express");

const router = express.Router();

// Import controllers
const {

    getStudents,

    getStudentById,

    createStudent,

    updateStudent,

    deleteStudent

} = require("../controllers/studentController");


// GET - All students
router.get("/", getStudents);


// GET - Single student
router.get("/:id", getStudentById);


// POST - Create student
router.post("/", createStudent);


// PUT - Update student
router.put("/:id", updateStudent);


// DELETE - Delete student
router.delete("/:id", deleteStudent);


// Export router
module.exports = router;
```

### 10.4 Create `server.js`

```
const express = require("express");

const app = express();

// Middleware to read JSON
app.use(express.json());

// Import student routes
const studentRoutes = require("./routes/studentRoutes");

// Register student routes
app.use("/api/students", studentRoutes);

// Default route
app.get("/", (req, res) => {

    res.send("Student Management API");

});

// Start server
app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

### 10.5 Test using Postman

| Method | URL               | Purpose          |
| ------ | ----------------- | ---------------- |
| GET    | `/api/students`   | Get all students |
| GET    | `/api/students/1` | Get one student  |
| POST   | `/api/students`   | Create student   |
| PUT    | `/api/students/1` | Update student   |
| DELETE | `/api/students/1` | Delete student   |

POST request body:

```
{
    "name": "Kiran",
    "email": "kiran@example.com"
}
```

PUT request body:

```
{
    "name": "Ramesh Kumar",
    "email": "rameshkumar@example.com"
}
```

### 10.6 Understand the CRUD flow

\#chatgpt-mermaid-\_r_6as\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_6as\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_6as\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_6as\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_6as\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6as\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_6as\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_6as\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_6as\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_6as\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_6as\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_6as\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_6as\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_6as\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_6as\_ p{margin:0;}#chatgpt-mermaid-\_r_6as\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6as\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6as\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6as\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_6as\_ .label text,#chatgpt-mermaid-\_r_6as\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6as\_ .node rect,#chatgpt-mermaid-\_r_6as\_ .node circle,#chatgpt-mermaid-\_r_6as\_ .node ellipse,#chatgpt-mermaid-\_r_6as\_ .node polygon,#chatgpt-mermaid-\_r_6as\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_6as\_ .rough-node .label text,#chatgpt-mermaid-\_r_6as\_ .node .label text,#chatgpt-mermaid-\_r_6as\_ .image-shape .label,#chatgpt-mermaid-\_r_6as\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_6as\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_6as\_ .rough-node .label,#chatgpt-mermaid-\_r_6as\_ .node .label,#chatgpt-mermaid-\_r_6as\_ .image-shape .label,#chatgpt-mermaid-\_r_6as\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_6as\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_6as\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_6as\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_6as\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_6as\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_6as\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_6as\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_6as\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_6as\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_6as\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_6as\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6as\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6as\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_6as\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6as\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_6as\_ .icon-shape,#chatgpt-mermaid-\_r_6as\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_6as\_ .icon-shape p,#chatgpt-mermaid-\_r_6as\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_6as\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_6as\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_6as\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_6as\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_6as\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_6as\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_6as\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_6as\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_6as\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_6as\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_6as\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_6as\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_6as\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_6as\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_6as\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_6as\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_6as\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_6as\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_6as\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_6as\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_6as\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_6as\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_6as\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_6as\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_6as\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_6as\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_6as\_ .node rect,#chatgpt-mermaid-\_r_6as\_ .node circle,#chatgpt-mermaid-\_r_6as\_ .node ellipse,#chatgpt-mermaid-\_r_6as\_ .node polygon,#chatgpt-mermaid-\_r_6as\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_6as\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_6as\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_6as\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_6as\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_6as\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Client RequestStudent RouteStudent ControllerHTTP MethodRead StudentsCreate StudentUpdate StudentDelete StudentJSON ResponseGETPOSTPUTDELETE

### 10.7 Important: What is the limitation of this example?

We are storing students in a JavaScript array.

That means:

- Data is stored only in server memory.
- Restarting the server resets the data.
- This is not permanent database storage.
- Multiple server instances will not share the same array.

Later, we will connect controllers to MongoDB or PostgreSQL.

## 11. Common mistakes

### Mistake 1 — Forgetting to export controller

Wrong:

```
const getStudents = (req, res) => {

    res.json([]);

};
```

Correct:

```
module.exports = {
    getStudents
};
```

### Mistake 2 — Incorrect controller import path

Wrong:

```
require("./studentController");
```

If the controller is inside the `controllers` folder, use:

```
require("../controllers/studentController");
```

The correct path depends on the file importing it.

### Mistake 3 — Calling the controller immediately

Wrong:

```
router.get("/", getStudents());
```

Correct:

```
router.get("/", getStudents);
```

Why? Express expects a function reference that it can execute when the request arrives.

### Mistake 4 — Forgetting `return` after an error response

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

res.json(student);
```

Without `return`, the function may continue and attempt to send another response.

### Mistake 5 — Mixing route and controller logic

Avoid putting all request-handling logic inside a large route file.

Prefer:

```
router.get("/", getStudents);
```

## 12. Best practices

1. Create separate controller files for each resource.
2. Use meaningful function names such as `getStudents` and `createStudent`.
3. Keep route files focused on endpoint definitions.
4. Use appropriate HTTP status codes.
5. Validate request data.
6. Handle errors properly.
7. Use `async/await` when working with databases.
8. Avoid hardcoding sensitive information.
9. Keep business logic separate when applications grow.
10. Return consistent JSON response structures.

### Recommended folder structure

```
backend/
│
├── config/
│   └── db.js
│
├── controllers/
│   ├── studentController.js
│   ├── userController.js
│   └── productController.js
│
├── routes/
│   ├── studentRoutes.js
│   ├── userRoutes.js
│   └── productRoutes.js
│
├── models/
│   ├── Student.js
│   ├── User.js
│   └── Product.js
│
├── middlewares/
│   ├── authMiddleware.js
│   └── errorMiddleware.js
│
├── services/
│
├── utils/
│
├── .env
├── .gitignore
├── package.json
└── server.js
```

### GitHub README image folder

When adding actual diagrams or handwritten notes to GitHub, use:

```
21_Express_Controllers/
│
├── images/
│   ├── controller-flow.png
│   └── project-structure.png
│
└── README.md
```

Add images using relative paths:

```
![Controller Flow](./images/controller-flow.png)

![Project Structure](./images/project-structure.png)
```

These images must be added to your repository. The Mermaid diagrams above can be pasted directly into GitHub README.

## 13. Interview questions

### Beginner level

Q1. What is a controller in Express.js?

A controller is a function responsible for handling an incoming request and sending an appropriate response.

Q2. Why do we use controllers?

To separate request-handling logic from route definitions and improve code organization.

Q3. What is the difference between routes and controllers?

Routes define the URL and HTTP method. Controllers handle the request when that route matches.

Q4. How do you export a controller?

```
module.exports = {
    getStudents
};
```

### Intermediate level

Q5. How do you connect a controller to a route?

```
router.get("/", getStudents);
```

Q6. Can one controller file contain multiple functions?

Yes. For example, `studentController.js` can contain `getStudents`, `createStudent`, `updateStudent`, and `deleteStudent`.

Q7. Why should we avoid writing all logic inside route files?

It makes files large and difficult to maintain, test, and debug.

Q8. What are `req.params` and `req.body` used for in controllers?

- `req.params`: Reads values from route parameters.
- `req.body`: Reads parsed request-body data.

### Advanced level

Q9. What is the difference between a controller and a service?

A controller manages HTTP request and response handling. A service contains reusable business operations, such as calculations, workflows, and data-related operations.

Q10. Should controllers directly communicate with the database?

They can in small applications. In larger applications, separating database operations into services or repositories can improve maintainability.

Q11. How do you handle asynchronous errors in controllers?

Use `try/catch` and pass errors to Express error middleware where needed. Express 5 automatically forwards rejected promises from returned async handlers.

Q12. How do you test controllers?

You can use unit testing tools such as Jest or Vitest and mock request, response, and service dependencies.

## 14. Practice problems

### Beginner exercises

1. Create a `studentController.js` file.
2. Create a `getStudents()` controller.
3. Create a `getStudentById()` controller.
4. Export both controller functions.
5. Connect both functions to student routes.

### Intermediate exercises

6. Create a `createStudent()` controller.
7. Create an `updateStudent()` controller.
8. Create a `deleteStudent()` controller.
9. Build a complete Student CRUD API using controllers.
10. Create separate employee and product controllers.

### Advanced exercises

11. Create controllers for a Book Management API.
12. Add request-body validation.
13. Handle missing IDs with a 404 response.
14. Use `async/await` in database-related controllers.
15. Create a reusable response format for all controllers.

## 15. Mini challenge — Employee Management CRUD API

Your task

Build an Employee Management API using separate routes and controllers.

### Requirements

Create these endpoints:

```
POST    /api/employees
GET     /api/employees
GET     /api/employees/:id
PUT     /api/employees/:id
DELETE  /api/employees/:id
```

### Employee fields

```
{
    "name": "Ramesh",
    "email": "ramesh@example.com",
    "salary": 30000,
    "department": "Development"
}
```

### Expected project structure

```
21_Express_Controllers/
│
├── controllers/
│   └── employeeController.js
│
├── routes/
│   └── employeeRoutes.js
│
├── server.js
│
└── package.json
```

### Your task

Try to implement:

1. `getEmployees()`
2. `getEmployeeById()`
3. `createEmployee()`
4. `updateEmployee()`
5. `deleteEmployee()`

Logic-building method:

For each function, follow these steps:

```
Requirement
    ↓
Input
    ↓
Find or Create Data
    ↓
Check Conditions
    ↓
Perform Operation
    ↓
Send Response
```

Try writing the functions yourself before checking the Student CRUD example.

## 16. Chapter summary

| Topic                     | What you learned                          |
| ------------------------- | ----------------------------------------- |
| Controller                | Handles request and response              |
| Controller function       | A function such as `getStudents()`        |
| Controller responsibility | Request handling                          |
| Route separation          | Separates endpoints from logic            |
| Request handling          | Reads data from `req`                     |
| Response handling         | Sends data using `res`                    |
| Export                    | Makes controller available to other files |
| Import                    | Connects controller to routes             |
| CRUD controllers          | Create, Read, Update, Delete              |

Main concept: Controllers separate request-handling logic from route definitions, making Express applications easier to maintain and develop.

## 17. Quick revision

🧠 Remember these important points

- Routes define API endpoints.
- Controllers handle incoming requests.
- `req` contains request information.
- `res` sends the response.
- Controllers can contain multiple functions.
- Export controllers using `module.exports`.
- Import controllers using `require()`.
- Connect controllers using `router.get()`, `router.post()`, etc.
- Use separate controller files for different resources.

  ⭐ Most important syntax

```
// studentController.js

const getStudents = (req, res) => {

    res.json({
        message: "All Students"
    });

};

module.exports = {
    getStudents
};
```

```
// studentRoutes.js

const express = require("express");

const router = express.Router();

const {
    getStudents
} = require("../controllers/studentController");

router.get("/", getStudents);

module.exports = router;
```

Chapter 21 completed

Practice: Try the Employee Management CRUD API mini challenge.

When you're ready, type `NEXT` to start Chapter 22 — Express Error Handling, where we will learn `try/catch`, custom errors, HTTP status codes, centralized error handling, and asynchronous error handling.