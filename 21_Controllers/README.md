# 🚀 PART 5 — EXPRESS.JS

# Chapter 21 — Express Controllers

BEGINNER LEVEL → PRACTICAL LEVEL

## 📚 Table of Contents

1. What is a Controller?
2. Why do we need Controllers?
3. Real-world Analogy
4. Routes vs Controllers
5. Controller Syntax
6. Basic Controller Example
7. Dry Run
8. Output
9. Line-by-Line Explanation
10. Practical Example — Student CRUD API
11. Understanding MVC Architecture
12. Common Mistakes
13. Best Practices
14. Interview Questions
15. Practice Problems
16. Mini Challenge
17. Chapter Summary & Quick Revision

## 1. 🧠 What is a Controller?

A Controller is a JavaScript function that handles the logic of an API request.

In simple words:

- Route: Decides which URL should be handled.
- Controller: Decides what to do when that URL is requested.

For example:

```
router.get("/students", getStudents);
```

Here:

- `/students` is the route.
- `getStudents` is the controller function.

The controller contains the actual logic for fetching student data and sending a response.

### Simple example

```
// Controller function
const getStudents = (req, res) => {

    res.send("All Students");

};
```

Main idea: Keep route definitions and request-handling logic separate.

## 2. 🤔 Why do we need Controllers?

Imagine your Student API has these routes:

```
GET     /students
GET     /students/:id
POST    /students
PUT     /students/:id
PATCH   /students/:id
DELETE  /students/:id
```

If you write all the logic inside the route file, it becomes large.

### Without Controllers

```
router.get("/students", (req, res) => {

    // 20 lines of logic

});

router.post("/students", (req, res) => {

    // 30 lines of logic

});

router.delete("/students/:id", (req, res) => {

    // 25 lines of logic

});
```

### With Controllers

studentRoutes.js

```
router.get("/", getStudents);

router.post("/", createStudent);

router.delete("/:id", deleteStudent);
```

studentController.js

```
const getStudents = (req, res) => {
    // Get student logic
};

const createStudent = (req, res) => {
    // Create student logic
};

const deleteStudent = (req, res) => {
    // Delete student logic
};
```

### Benefits

1. Code becomes clean.
2. Code becomes reusable.
3. Easier debugging.
4. Easier testing.
5. Easier project maintenance.
6. Better separation of responsibilities.

## 3. 🌍 Real-world Analogy

Imagine a restaurant.

```
CUSTOMER
   |
   v
WAITER
   |
   v
KITCHEN
   |
   v
CHEF PREPARES FOOD
   |
   v
WAITER SERVES FOOD
```

Think of it this way:

| Restaurant       | Express        |
| ---------------- | -------------- |
| Customer request | Client request |
| Waiter           | Route          |
| Chef             | Controller     |
| Prepared food    | API response   |

The route receives the request and directs it to the correct controller.

The controller performs the required operation and sends the response.

## 4. 🔄 Routes vs Controllers

This is one of the most important concepts.

| Routes                      | Controllers                      |
| --------------------------- | -------------------------------- |
| Define API endpoints        | Handle request logic             |
| Connect URL to handler      | Perform actual operations        |
| Usually stored in `routes/` | Usually stored in `controllers/` |
| Use `router.get()`          | Use JavaScript functions         |
| Example: `/students`        | Example: `getStudents`           |

### Request flow

```
CLIENT
  |
  v
GET /api/students
  |
  v
studentRoutes.js
  |
  | router.get("/", getStudents)
  v
studentController.js
  |
  | Fetch student data
  v
Send JSON Response
  |
  v
CLIENT
```

## 5. 📝 Controller Syntax

### Step 1: Create controller function

```
const getStudents = (req, res) => {

    res.json({
        message: "Students fetched successfully"
    });

};
```

### Step 2: Export controller function

```
module.exports = {
    getStudents
};
```

### Step 3: Import controller into routes

```
const {
    getStudents
} = require("../controllers/studentController");
```

### Step 4: Connect controller to route

```
router.get("/", getStudents);
```

That's it!

The route calls the controller when a matching request arrives.

## 6. 💻 Basic Controller Example

Let's create a small project.

### Project structure

```
controller-demo/
│
├── server.js
│
├── routes/
│   └── studentRoutes.js
│
└── controllers/
    └── studentController.js
```

### Step 1: Install Express

```
npm init -y
npm install express
```

### Step 2: Create `controllers/studentController.js`

```
// Controller function
const getStudents = (req, res) => {

    res.send("All Students");

};

// Export controller
module.exports = {
    getStudents
};
```

### Step 3: Create `routes/studentRoutes.js`

```
// Import Express
const express = require("express");

// Create Router
const router = express.Router();

// Import controller
const {
    getStudents
} = require("../controllers/studentController");

// Create route
router.get("/", getStudents);

// Export router
module.exports = router;
```

### Step 4: Create `server.js`

```
// Import Express
const express = require("express");

// Create application
const app = express();

// Import student routes
const studentRoutes = require("./routes/studentRoutes");

// Register routes
app.use("/api/students", studentRoutes);

// Start server
app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

### Step 5: Run server

```
node server.js
```

Open:

```
http://localhost:3000/api/students
```

## 7. 🔍 Dry Run

Let's understand how the request works.

Request:

```
GET http://localhost:3000/api/students
```

Step 1: Express receives the request.

Step 2: `server.js` forwards it to the student router.

```
app.use("/api/students", studentRoutes);
```

Step 3: Router matches the path `/`.

```
router.get("/", getStudents);
```

Step 4: Express executes the controller.

```
const getStudents = (req, res) => {

    res.send("All Students");

};
```

Step 5: Controller sends the response.

## 8. 📤 Output

Expected output

Browser / Postman:

```
All Students
```

Terminal:

```
Server running on port 3000
```

## 9. 🔎 Line-by-Line Explanation

Let's understand these important lines.

### Controller

```
const getStudents = (req, res) => {
```

Creates a function named `getStudents`.

```
res.send("All Students");
```

Sends a response to the client.

```
module.exports = {
    getStudents
};
```

Exports the function so another file can use it.

### Routes

```
const {
    getStudents
} = require("../controllers/studentController");
```

Imports the exported controller function.

```
router.get("/", getStudents);
```

Connects the GET route to the controller.

Important: We write `getStudents`, not `getStudents()`.

Why?

- `getStudents` passes the function to Express.
- `getStudents()` executes the function immediately.

## 10. 🏗️ Practical Example — Complete Student CRUD API

Now let's build a real CRUD API using separate:

- Data file
- Route file
- Controller file
- Server file

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
└── controllers/
    └── studentController.js
```

### Step 2: Create `data/students.js`

This file stores our raw student data.

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

// Export students array
module.exports = students;
```

### Step 3: Create `controllers/studentController.js`

This file contains all CRUD logic.

```
// Import student data
const students = require("../data/students");

// ======================================
// GET: Fetch all students
// ======================================

const getStudents = (req, res) => {

    res.status(200).json({

        message: "Students fetched successfully",

        data: students

    });

};

// ======================================
// GET: Fetch student by ID
// ======================================

const getStudentById = (req, res) => {

    // Get ID from URL
    const id = Number(req.params.id);

    // Find student
    const student = students.find((item) => item.id === id);

    // Check student exists
    if (!student) {

        return res.status(404).json({

            message: "Student not found"

        });

    }

    // Send student data
    res.status(200).json({

        message: "Student found",

        data: student

    });

};

// ======================================
// POST: Create new student
// ======================================

const createStudent = (req, res) => {

    // Get data from request body
    const { name, course, age } = req.body;

    // Validate input
    if (!name || !course || age === undefined) {

        return res.status(400).json({

            message: "Name, course and age are required"

        });

    }

    // Create new student
    const newStudent = {

        id: students.length
            ? Math.max(...students.map((item) => item.id)) + 1
            : 1,

        name,
        course,
        age

    };

    // Add student to array
    students.push(newStudent);

    // Send response
    res.status(201).json({

        message: "Student created successfully",

        data: newStudent

    });

};

// ======================================
// PUT: Update complete student
// ======================================

const updateStudent = (req, res) => {

    // Get ID from URL
    const id = Number(req.params.id);

    // Find array index
    const index = students.findIndex((item) => item.id === id);

    // Check student
    if (index === -1) {

        return res.status(404).json({

            message: "Student not found"

        });

    }

    // Get new data
    const { name, course, age } = req.body;

    // Validate input
    if (!name || !course || age === undefined) {

        return res.status(400).json({

            message: "Name, course and age are required"

        });

    }

    // Replace complete student object
    students[index] = {

        id,
        name,
        course,
        age

    };

    // Send updated data
    res.status(200).json({

        message: "Student updated successfully",

        data: students[index]

    });

};

// ======================================
// PATCH: Update selected fields
// ======================================

const updateStudentPartially = (req, res) => {

    const id = Number(req.params.id);

    // Find student
    const student = students.find((item) => item.id === id);

    if (!student) {

        return res.status(404).json({

            message: "Student not found"

        });

    }

    // Read fields from request body
    const { name, course, age } = req.body;

    // Update only provided fields
    if (name !== undefined) student.name = name;

    if (course !== undefined) student.course = course;

    if (age !== undefined) student.age = age;

    // Send updated student
    res.status(200).json({

        message: "Student partially updated",

        data: student

    });

};

// ======================================
// DELETE: Delete student
// ======================================

const deleteStudent = (req, res) => {

    const id = Number(req.params.id);

    // Find student index
    const index = students.findIndex((item) => item.id === id);

    // Check student
    if (index === -1) {

        return res.status(404).json({

            message: "Student not found"

        });

    }

    // Remove student from array
    const deletedStudent = students.splice(index, 1)[0];

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
    updateStudentPartially,
    deleteStudent

};
```

### Step 4: Create `routes/studentRoutes.js`

Notice that this file contains only route definitions.

```
// Import Express
const express = require("express");

// Create Router
const router = express.Router();

// Import controller functions
const {

    getStudents,
    getStudentById,
    createStudent,
    updateStudent,
    updateStudentPartially,
    deleteStudent

} = require("../controllers/studentController");

// GET: All students
router.get("/", getStudents);

// GET: Student by ID
router.get("/:id", getStudentById);

// POST: Create student
router.post("/", createStudent);

// PUT: Update complete student
router.put("/:id", updateStudent);

// PATCH: Update selected fields
router.patch("/:id", updateStudentPartially);

// DELETE: Delete student
router.delete("/:id", deleteStudent);

// Export router
module.exports = router;
```

### Step 5: Create `server.js`

This file connects everything.

```
// Import Express
const express = require("express");

// Create application
const app = express();

// Port number
const PORT = 3000;

// Middleware to read JSON data
app.use(express.json());

// Import student routes
const studentRoutes = require("./routes/studentRoutes");

// Connect student routes
app.use("/api/students", studentRoutes);

// Start server
app.listen(PORT, () => {

    console.log(`Server running on port ${PORT}`);

});
```

### Step 6: Understand the complete request flow

```
CLIENT
  |
  | POST /api/students
  v
server.js
  |
  | app.use("/api/students", studentRoutes)
  v
studentRoutes.js
  |
  | router.post("/", createStudent)
  v
studentController.js
  |
  | Read req.body
  | Validate data
  | Create student object
  | students.push(newStudent)
  v
Send JSON Response
  |
  v
CLIENT
```

### Step 7: Test with Postman

1\. GET all students

```
GET http://localhost:3000/api/students
```

2\. GET student by ID

```
GET http://localhost:3000/api/students/1
```

3\. POST new student

```
POST http://localhost:3000/api/students
```

Body → raw → JSON:

```
{
    "name": "Anil",
    "course": "FastAPI",
    "age": 23
}
```

4\. PUT complete student

```
PUT http://localhost:3000/api/students/1
```

Body:

```
{
    "name": "Ramesh Kumar",
    "course": "Full Stack",
    "age": 26
}
```

5\. PATCH selected field

```
PATCH http://localhost:3000/api/students/1
```

Body:

```
{
    "course": "Machine Learning"
}
```

6\. DELETE student

```
DELETE http://localhost:3000/api/students/2
```

### Step 8: Understand raw data changes

Initial data:

```
[
    { id: 1, name: "Ramesh", course: "Node.js", age: 25 },
    { id: 2, name: "Kumar", course: "React.js", age: 24 },
    { id: 3, name: "Suresh", course: "Python", age: 26 }
]
```

After POST:

```
[
    { id: 1, name: "Ramesh", course: "Node.js", age: 25 },
    { id: 2, name: "Kumar", course: "React.js", age: 24 },
    { id: 3, name: "Suresh", course: "Python", age: 26 },
    { id: 4, name: "Anil", course: "FastAPI", age: 23 }
]
```

After PATCH student 1:

```
[
    { id: 1, name: "Ramesh", course: "Machine Learning", age: 25 },
    { id: 2, name: "Kumar", course: "React.js", age: 24 },
    { id: 3, name: "Suresh", course: "Python", age: 26 },
    { id: 4, name: "Anil", course: "FastAPI", age: 23 }
]
```

After DELETE student 2:

```
[
    { id: 1, name: "Ramesh", course: "Machine Learning", age: 25 },
    { id: 3, name: "Suresh", course: "Python", age: 26 },
    { id: 4, name: "Anil", course: "FastAPI", age: 23 }
]
```

Important: This example uses an in-memory array. Data will reset when the server restarts. Later, we will use MongoDB to store data permanently.

## 11. 🏛️ Understanding MVC Architecture

MVC stands for:

- M — Model
- V — View
- C — Controller

It is an architectural pattern used to organize application code.

### What is Model?

Model handles the data and database-related operations.

Example:

```
models/
    Student.js
```

Later, we will use Mongoose models to communicate with MongoDB.

### What is View?

View is the user interface that displays information.

For example, in a full-stack application, React can be the frontend view.

In a JSON REST API, the server commonly sends JSON responses instead of rendering HTML views.

### What is Controller?

Controller handles the request and coordinates the required operations.

Example:

```
controllers/
    studentController.js
```

### MVC flow

```
CLIENT / REACT FRONTEND
         |
         v
       ROUTE
         |
         v
     CONTROLLER
         |
         v
       MODEL
         |
         v
      DATABASE
         |
         v
     CONTROLLER
         |
         v
    JSON RESPONSE
         |
         v
       CLIENT
```

### Recommended MVC-style project structure

```
student-management/
│
├── server.js
│
├── config/
│   └── db.js
│
├── models/
│   └── Student.js
│
├── routes/
│   └── studentRoutes.js
│
├── controllers/
│   └── studentController.js
│
├── middleware/
│   └── authMiddleware.js
│
├── .env
│
└── package.json
```

## 12. ⚠️ Common Mistakes

### Mistake 1: Forgetting to export controller functions

Incorrect:

```
const getStudents = (req, res) => {
    res.send("Students");
};
```

Correct:

```
module.exports = {
    getStudents
};
```

### Mistake 2: Wrong controller import path

Incorrect:

```
require("./controllers/studentController");
```

This path may be incorrect when importing from inside the `routes` folder.

Correct:

```
require("../controllers/studentController");
```

### Mistake 3: Calling the controller immediately

Incorrect:

```
router.get("/", getStudents());
```

Correct:

```
router.get("/", getStudents);
```

### Mistake 4: Typing different function names

Controller export:

```
module.exports = {
    getStudents
};
```

Route import must use the same name:

```
const { getStudents } = require("../controllers/studentController");
```

### Mistake 5: Putting all business logic back into routes

Avoid this:

```
router.get("/", (req, res) => {

    // Large amount of logic here

});
```

Prefer:

```
router.get("/", getStudents);
```

## 13. ⭐ Best Practices

- Keep route files small.
- Keep request-handling logic in controllers.
- Use meaningful function names.
- Use proper HTTP status codes.
- Validate incoming data.
- Handle errors consistently.
- Keep database logic organized in models or service layers as projects grow.
- Avoid putting secrets directly in source code.
- Use a consistent naming convention.

### Routes should look simple

```
router.get("/", getStudents);

router.post("/", createStudent);

router.put("/:id", updateStudent);

router.delete("/:id", deleteStudent);
```

### Controllers should contain logic

```
const getStudents = (req, res) => {

    // Fetch students

};
```

## 14. 🎯 Interview Questions

## 15. 📝 Practice Problems

Try these exercises.

- Problem 1: Create `productController.js` with a `getProducts` function.
- Problem 2: Create `productRoutes.js` and connect the controller.
- Problem 3: Create `employeeController.js` with GET and POST functions.
- Problem 4: Create a separate data file for employees.
- Problem 5: Build a complete Product CRUD API using controllers.
- Problem 6: Create an MVC-style folder structure for a Student Management API.

## 16. 🏆 Mini Challenge — Employee Management API

### Requirement

Create an Employee Management API using separate route and controller files.

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

### Expected project structure

```
employee-api/
│
├── server.js
│
├── data/
│   └── employees.js
│
├── routes/
│   └── employeeRoutes.js
│
└── controllers/
    └── employeeController.js
```

### Your tasks

1. Create an employee data file.
2. Create `employeeController.js`.
3. Create `getEmployees`.
4. Create `getEmployeeById`.
5. Create `createEmployee`.
6. Create `deleteEmployee`.
7. Export all controller functions.
8. Import controllers in `employeeRoutes.js`.
9. Connect the router in `server.js`.

### Expected URLs

```
GET     /api/employees
GET     /api/employees/1
POST    /api/employees
DELETE  /api/employees/1
```

### Logic-building steps

Step 1 — Requirement: Separate Employee API routes and controllers.

Step 2 — Input: Employee ID and employee details.

Step 3 — Output: JSON responses containing employee data.

Step 4 — Break into steps:

```
Create Data
    |
    v
Create Controller
    |
    v
Create Routes
    |
    v
Connect in server.js
    |
    v
Test using Postman
```

Step 5 — Hint:

```
const getEmployees = (req, res) => {

    // Your logic

};
```

Step 6 — Pseudocode:

```
START

Import employee data

Create GET controller
Create GET by ID controller
Create POST controller
Create DELETE controller

Export controllers

Import controllers in routes

Connect routes to server

END
```

Step 7 — Your turn!

Try writing the code yourself. Send your attempt, and I will check it line by line.

## 17. 📌 Chapter Summary & Quick Revision

### What did we learn?

| Concept          | Meaning                              |
| ---------------- | ------------------------------------ |
| Controller       | Handles API request logic            |
| Route            | Defines API endpoint                 |
| Model            | Handles data and database operations |
| View             | Displays information                 |
| MVC              | Model, View, Controller              |
| `module.exports` | Exports functions                    |
| `require()`      | Imports functions                    |
| `req`            | Request information                  |
| `res`            | Response object                      |

### Final request flow

```
CLIENT
  |
  v
SERVER.JS
  |
  v
ROUTES
  |
  v
CONTROLLERS
  |
  v
MODELS
  |
  v
DATABASE
  |
  v
JSON RESPONSE
  |
  v
CLIENT
```

### Self-check

- I understand what a Controller is.
- I understand Routes vs Controllers.
- I can create controller functions.
- I can export and import controllers.
- I can connect controllers to routes.
- I understand MVC architecture.
- I can build a CRUD API using separate files.

## 🎓 Next Chapter

Chapter 22 — Express Error Handling

We will learn:

- What is Error Handling?
- Why do we need it?
- Types of errors
- `try...catch`
- `throw new Error()`
- `next(error)`
- Error-handling middleware
- Custom error messages
- HTTP status codes
- Practical Student API error handling

Type `NEXT` to start Chapter 22.