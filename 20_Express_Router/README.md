# 🚀 PART 5 — EXPRESS.JS

# Chapter 20 — Express Router

BEGINNER LEVEL → PRACTICAL LEVEL

## 📚 Table of Contents

1. What is Express Router?
2. Why do we need Express Router?
3. Real-world Analogy
4. Express Router Architecture
5. Router Syntax
6. Basic Router Example
7. Dry Run
8. Output
9. Line-by-Line Explanation
10. Practical Example — Student API
11. HTTP Methods in Router
12. Common Mistakes
13. Best Practices
14. Interview Questions
15. Practice Problems
16. Mini Challenge
17. Chapter Summary & Quick Revision

## 1. 🧠 What is Express Router?

Express Router is a tool that helps us organize API routes into separate files.

In simple words:

Instead of writing all API routes inside `server.js`, we can create separate files for different modules.

For example:

- Student routes
- Employee routes
- Product routes
- Order routes
- User routes

Express Router helps us manage these routes easily.

### Without Express Router

All routes are inside one file.

```
project/
│
└── server.js
    ├── Student Routes
    ├── Employee Routes
    ├── Product Routes
    ├── Order Routes
    └── User Routes
```

As the project grows, `server.js` becomes very large.

### With Express Router

We separate routes into different files.

```
project/
│
├── server.js
│
└── routes/
    ├── studentRoutes.js
    ├── employeeRoutes.js
    ├── productRoutes.js
    ├── orderRoutes.js
    └── userRoutes.js
```

Main idea: One module = One route file.

## 2. 🤔 Why do we need Express Router?

Imagine you are building a Student Management System.

You need these APIs:

| Module    | API          |
| --------- | ------------ |
| Students  | `/students`  |
| Employees | `/employees` |
| Products  | `/products`  |
| Orders    | `/orders`    |
| Users     | `/users`     |

If you write every route inside `server.js`, it becomes difficult to maintain.

Express Router solves this problem.

### Benefits

1. Code organization: Separate routes into different files.
2. Reusability: Router middleware can be applied to a group of routes.
3. Maintainability: Easier to update and debug.
4. Scalability: Easier to add new modules.
5. Readability: Cleaner project structure.

## 3. 🌍 Real-world Analogy

Imagine a college with different departments.

```
COLLEGE
  |
  +---- Computer Science Department
  |          |
  |          +---- Students
  |          +---- Teachers
  |
  +---- Commerce Department
  |          |
  |          +---- Students
  |          +---- Teachers
  |
  +---- Science Department
             |
             +---- Students
             +---- Teachers
```

Each department manages its own work.

Express Router works similarly.

```
EXPRESS SERVER
      |
      +---- studentRoutes.js
      |
      +---- employeeRoutes.js
      |
      +---- productRoutes.js
      |
      +---- orderRoutes.js
```

Each route file manages its own API endpoints.

## 4. 🔄 Express Router Architecture

Let's understand how a request travels through the application.

```
CLIENT
  |
  | GET /api/students
  v
server.js
  |
  | app.use("/api", studentRoutes)
  v
studentRoutes.js
  |
  | router.get("/students", ...)
  v
ROUTE HANDLER
  |
  v
JSON RESPONSE
  |
  v
CLIENT
```

### Important concept

In `server.js`:

```
app.use("/api", studentRoutes);
```

In `studentRoutes.js`:

```
router.get("/students", ...);
```

The final URL is:

```
/api + /students

/api/students
```

## 5. 📝 Router Syntax

### Step 1: Import Express

```
const express = require("express");
```

### Step 2: Create Router

```
const router = express.Router();
```

### Step 3: Create routes

```
router.get("/students", (req, res) => {

    res.send("All Students");

});
```

### Step 4: Export Router

```
module.exports = router;
```

### Step 5: Import Router in `server.js`

```
const studentRoutes = require("./routes/studentRoutes");
```

### Step 6: Register Router

```
app.use("/api", studentRoutes);
```

## 6. 💻 Basic Router Example

Let's create a simple project.

### Project structure

```
express-router-demo/
│
├── server.js
│
└── routes/
    └── studentRoutes.js
```

### Step 1: Install Express

```
npm init -y
npm install express
```

### Step 2: Create `routes/studentRoutes.js`

```
// Import Express
const express = require("express");

// Create Router
const router = express.Router();

// GET route
router.get("/students", (req, res) => {

    res.send("All Students");

});

// Export Router
module.exports = router;
```

### Step 3: Create `server.js`

```
// Import Express
const express = require("express");

// Create Express application
const app = express();

// Import student routes
const studentRoutes = require("./routes/studentRoutes");

// Register student routes
app.use("/api", studentRoutes);

// Start server
app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

### Step 4: Run server

```
node server.js
```

Open:

```
http://localhost:3000/api/students
```

## 7. 🔍 Dry Run

Let's understand the execution.

Request:

```
GET http://localhost:3000/api/students
```

### Step-by-step execution

Step 1: Client sends a request.

```
GET /api/students
```

Step 2: Express receives the request in `server.js`.

```
app.use("/api", studentRoutes);
```

Express checks whether the request URL starts with `/api`.

Step 3: Express forwards the matching request to `studentRoutes`.

Step 4: Router checks its route:

```
router.get("/students", ...);
```

Step 5: The route handler executes.

```
res.send("All Students");
```

Step 6: Server sends the response.

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

Let's understand the most important lines.

### In `studentRoutes.js`

```
const express = require("express");
```

Imports Express.

```
const router = express.Router();
```

Creates a new Router object.

Think of this router as a small route manager.

```
router.get("/students", (req, res) => {
    res.send("All Students");
});
```

Creates a GET route inside the router.

```
module.exports = router;
```

Exports the router so another file can use it.

### In `server.js`

```
const studentRoutes = require("./routes/studentRoutes");
```

Imports the router file.

```
app.use("/api", studentRoutes);
```

Connects the student router to the `/api` base path.

Remember: The router's route path is added to the base path.

## 10. 🏗️ Practical Example — Student CRUD API

Now let's create a complete Student CRUD API using Express Router and raw JavaScript data.

We will use:

- GET — Read students
- GET by ID — Read one student
- POST — Create student
- PUT — Update complete student
- PATCH — Update selected fields
- DELETE — Delete student

### Step 1: Project structure

```
student-api/
│
├── server.js
│
├── routes/
│   └── studentRoutes.js
│
└── data/
    └── students.js
```

### Step 2: Create `data/students.js`

This file contains our raw student data.

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

// Export student data
module.exports = students;
```

What is happening here?

We created an array containing three student objects.

Each student has:

- `id`
- `name`
- `course`
- `age`

We export the array so the route file can access it.

### Step 3: Create `routes/studentRoutes.js`

```
// Import Express
const express = require("express");

// Create Router
const router = express.Router();

// Import student data
const students = require("../data/students");

// ===================================
// GET: Fetch all students
// ===================================

router.get("/", (req, res) => {

    res.status(200).json({
        message: "Students fetched successfully",
        data: students
    });

});

// ===================================
// GET: Fetch student by ID
// ===================================

router.get("/:id", (req, res) => {

    // Get ID from URL
    const id = Number(req.params.id);

    // Find student
    const student = students.find((item) => item.id === id);

    // Check student
    if (!student) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    // Send student
    res.status(200).json({
        message: "Student found",
        data: student
    });

});

// ===================================
// POST: Create new student
// ===================================

router.post("/", (req, res) => {

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

});

// ===================================
// PUT: Update complete student
// ===================================

router.put("/:id", (req, res) => {

    const id = Number(req.params.id);

    const index = students.findIndex((item) => item.id === id);

    if (index === -1) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    const { name, course, age } = req.body;

    if (!name || !course || age === undefined) {

        return res.status(400).json({
            message: "Name, course and age are required"
        });

    }

    students[index] = {
        id,
        name,
        course,
        age
    };

    res.status(200).json({
        message: "Student updated successfully",
        data: students[index]
    });

});

// ===================================
// PATCH: Update selected fields
// ===================================

router.patch("/:id", (req, res) => {

    const id = Number(req.params.id);

    const student = students.find((item) => item.id === id);

    if (!student) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    const { name, course, age } = req.body;

    if (name !== undefined) student.name = name;

    if (course !== undefined) student.course = course;

    if (age !== undefined) student.age = age;

    res.status(200).json({
        message: "Student partially updated",
        data: student
    });

});

// ===================================
// DELETE: Delete student
// ===================================

router.delete("/:id", (req, res) => {

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

// Export Router
module.exports = router;
```

### Step 4: Create `server.js`

```
// Import Express
const express = require("express");

// Create Express application
const app = express();

// Port number
const PORT = 3000;

// Parse JSON request body
app.use(express.json());

// Import student routes
const studentRoutes = require("./routes/studentRoutes");

// Register student routes
app.use("/api/students", studentRoutes);

// Start server
app.listen(PORT, () => {

    console.log(`Server running on port ${PORT}`);

});
```

### Step 5: Understand the final API URLs

Because we registered:

```
app.use("/api/students", studentRoutes);
```

And inside the router we created:

```
router.get("/");
router.get("/:id");
router.post("/");
router.put("/:id");
router.patch("/:id");
router.delete("/:id");
```

The final URLs are:

| Method | URL               | Purpose                |
| ------ | ----------------- | ---------------------- |
| GET    | `/api/students`   | Get all students       |
| GET    | `/api/students/1` | Get student by ID      |
| POST   | `/api/students`   | Create student         |
| PUT    | `/api/students/1` | Replace student        |
| PATCH  | `/api/students/1` | Update selected fields |
| DELETE | `/api/students/1` | Delete student         |

### Step 6: Test using Postman

1\. GET — All students

```
GET http://localhost:3000/api/students
```

2\. GET — Student by ID

```
GET http://localhost:3000/api/students/1
```

3\. POST — Create student

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

4\. PUT — Update complete student

```
PUT http://localhost:3000/api/students/1
```

Body:

```
{
    "name": "Ramesh Kumar",
    "course": "Full Stack Development",
    "age": 26
}
```

5\. PATCH — Update only course

```
PATCH http://localhost:3000/api/students/1
```

Body:

```
{
    "course": "Machine Learning"
}
```

6\. DELETE — Delete student

```
DELETE http://localhost:3000/api/students/2
```

### Step 7: Understand raw data changes

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

After PATCH on student 1:

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

Important: This data is stored only in memory. It resets when you restart the server. Later, we will connect MongoDB to store data permanently.

## 11. 🔧 HTTP Methods in Router

Express Router supports the same HTTP methods as the Express application.

| Router method     | Meaning          | Example                 |
| ----------------- | ---------------- | ----------------------- |
| `router.get()`    | Read data        | Get students            |
| `router.post()`   | Create data      | Add student             |
| `router.put()`    | Replace data     | Update complete student |
| `router.patch()`  | Partially update | Update course           |
| `router.delete()` | Delete data      | Remove student          |

Example:

```
router.get("/", getStudents);

router.post("/", createStudent);

router.put("/:id", updateStudent);

router.patch("/:id", updateStudentPartially);

router.delete("/:id", deleteStudent);
```

Here, `getStudents`, `createStudent`, and other functions are handler functions. We will learn how to move these functions into separate controller files in Chapter 21.

## 12. ⚠️ Common Mistakes

### Mistake 1: Forgetting to export the router

Incorrect:

```
const router = express.Router();

router.get("/", (req, res) => {
    res.send("Hello");
});
```

Correct:

```
module.exports = router;
```

### Mistake 2: Forgetting to import the router

Incorrect:

```
app.use("/api/students", studentRoutes);
```

If `studentRoutes` was never imported, Node.js will throw an error.

Correct:

```
const studentRoutes = require("./routes/studentRoutes");

app.use("/api/students", studentRoutes);
```

### Mistake 3: Incorrect route URL

Suppose:

```
app.use("/api/students", studentRoutes);
```

And:

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
/api/students/students
```

### Mistake 4: Wrong import path

Incorrect:

```
const studentRoutes = require("./studentRoutes");
```

Correct for our folder structure:

```
const studentRoutes = require("./routes/studentRoutes");
```

### Mistake 5: Registering JSON middleware after routes

Incorrect:

```
app.use("/api/students", studentRoutes);

app.use(express.json());
```

Correct:

```
app.use(express.json());

app.use("/api/students", studentRoutes);
```

## 13. ⭐ Best Practices

1. Create separate route files for each module.
2. Keep `server.js` clean.
3. Use meaningful route filenames.
4. Use a common base URL for related routes.
5. Keep route definitions separate from business logic as your application grows.
6. Register middleware before routes when the routes need it.
7. Use consistent naming conventions.

### Recommended project structure

```
student-management/
│
├── server.js
│
├── routes/
│   ├── studentRoutes.js
│   ├── employeeRoutes.js
│   └── userRoutes.js
│
├── controllers/
│   ├── studentController.js
│   ├── employeeController.js
│   └── userController.js
│
├── middleware/
│   ├── authMiddleware.js
│   └── errorMiddleware.js
│
├── models/
│
├── config/
│
├── .env
│
└── package.json
```

## 14. 🎯 Interview Questions

## 15. 📝 Practice Problems

Try these exercises.

- Problem 1: Create `productRoutes.js` and add a GET route.
- Problem 2: Create `employeeRoutes.js` and add GET and POST routes.
- Problem 3: Create `userRoutes.js` and add GET by ID.
- Problem 4: Connect all three routers in `server.js`.
- Problem 5: Create a separate data file for product data.
- Problem 6: Build a complete Product CRUD API using Express Router.

## 16. 🏆 Mini Challenge — Employee Management API

### Requirement

Create a modular Employee API using Express Router.

### Project structure

```
employee-api/
│
├── server.js
│
├── routes/
│   └── employeeRoutes.js
│
└── data/
    └── employees.js
```

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

1. Create a separate employee data file.
2. Create `employeeRoutes.js`.
3. Create GET all employees.
4. Create GET employee by ID.
5. Create POST employee.
6. Create DELETE employee.
7. Connect the router in `server.js`.

### Expected URLs

```
GET     /api/employees
GET     /api/employees/1
POST    /api/employees
DELETE  /api/employees/1
```

### Logic-building steps

Step 1 — Requirement: Build Employee CRUD routes.

Step 2 — Input: Employee ID and employee details.

Step 3 — Output: Employee records in JSON format.

Step 4 — Break into steps: Create data file → create router → create routes → connect router.

Step 5 — Hint:

```
const router = express.Router();

module.exports = router;
```

Step 6 — Pseudocode:

```
START

Import Express
Create Router
Import Employee Data

Create GET route
Create GET by ID route
Create POST route
Create DELETE route

Export Router

END
```

Step 7 — Your turn!

Try to complete the challenge. Send your code, and I will review it step by step. I won't reveal the full challenge solution unless you ask.

## 17. 📌 Chapter Summary & Quick Revision

### What did we learn?

| Concept            | Meaning                                |
| ------------------ | -------------------------------------- |
| Express Router     | Organizes routes into separate modules |
| `express.Router()` | Creates a router                       |
| `router.get()`     | Creates GET route                      |
| `router.post()`    | Creates POST route                     |
| `router.put()`     | Creates PUT route                      |
| `router.patch()`   | Creates PATCH route                    |
| `router.delete()`  | Creates DELETE route                   |
| `module.exports`   | Exports router                         |
| `require()`        | Imports router                         |
| `app.use()`        | Connects router to application         |

### Final request flow

```
CLIENT
  |
  v
server.js
  |
  v
app.use("/api/students", studentRoutes)
  |
  v
studentRoutes.js
  |
  v
ROUTE HANDLER
  |
  v
JSON RESPONSE
```

### Self-check

- I understand Express Router.
- I can create a router.
- I can export and import a router.
- I can connect routes in `server.js`.
- I can create separate route files.
- I understand the final API URL.
- I can build a basic CRUD API using Router.

## 🎓 Next Chapter

Chapter 21 — Express Controllers

We will learn:

- What is a Controller?
- Why do we need Controllers?
- Routes vs Controllers
- Creating controller files
- Exporting and importing controller functions
- Moving CRUD logic from routes to controllers
- Complete Student Management API
- Clean MVC-style project structure

Type `NEXT` to start Chapter 21.