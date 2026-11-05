# 🚀 PART 5 — EXPRESS.JS

# Chapter 18 — Express Routing

Beginner to Advanced • Practical Examples • Raw Data • GitHub README Notes

In this chapter, we will learn how to create API endpoints and perform CRUD operations using real JavaScript data.

I will explain each operation using a simple Student Management System. We will start with raw data (a JavaScript array), understand how the data changes, and then connect it to Express routes.

## 📚 Table of Contents

1. What is Express Routing?
2. Why Do We Need Routing?
3. Real-World Analogy
4. Architecture and Request Flow
5. HTTP Methods and Syntax
6. Basic Examples
7. Dry Run
8. Expected Outputs
9. Request Data: params, query, body
10. Practical Project — Student CRUD API
11. Common Mistakes
12. Best Practices
13. Interview Questions
14. Practice Problems
15. Mini Challenge
16. Chapter Summary
17. Quick Revision

## 🔑 Before Starting

You should understand these basic concepts:

| Concept        | Simple meaning                               |
| -------------- | -------------------------------------------- |
| Node.js        | Runs JavaScript outside the browser          |
| Express.js     | Framework used to build web servers and APIs |
| `express()`    | Creates an Express application               |
| `app.listen()` | Starts the server                            |
| HTTP           | Communication between client and server      |
| JSON           | Format used to exchange data                 |
| Function       | Reusable block of code                       |
| Array          | Stores multiple values                       |
| Object         | Stores data using key-value pairs            |

### Quick revision from Chapter 17

```
const express = require("express");

const app = express();

app.get("/", (req, res) => {

    res.send("Welcome to Express");

});

app.listen(3000);
```

- `express()` creates the application.
- `app.get()` creates a GET route.
- `/` is the URL path.
- `req` contains request information.
- `res` sends the response.
- `app.listen(3000)` starts the server on port 3000.

## 1. 🧠 What is Express Routing?

Definition: Express Routing is the process of defining how an application responds to different URLs and HTTP methods.

In simple words:

Routing decides which code should execute when a client requests a particular URL.

### Example

Imagine you are developing a Student Management API.

You need different operations:

| URL           | Purpose          |
| ------------- | ---------------- |
| `/students`   | Get all students |
| `/students/1` | Get one student  |
| `/students`   | Create a student |
| `/students/1` | Update a student |
| `/students/1` | Delete a student |

But how does Express understand which operation to perform?

It checks two things:

1. HTTP method — GET, POST, PUT, PATCH or DELETE.
2. URL path — `/students`, `/students/1`, etc.

### Basic syntax

```
app.METHOD(PATH, HANDLER);
```

Where:

| Part      | Meaning                             |
| --------- | ----------------------------------- |
| `app`     | Express application                 |
| `METHOD`  | HTTP method                         |
| `PATH`    | URL path                            |
| `HANDLER` | Function that processes the request |

Example:

```
app.get("/students", (req, res) => {

    res.send("Student List");

});
```

When a GET request comes to `/students`, Express executes this function.

## 2. ❓ Why Do We Need Routing?

Imagine you are building an application with these operations:

1. Get all students.
2. Get one student.
3. Create a student.
4. Update a student.
5. Delete a student.

Without Express routing, you may need to check the URL and method manually using many `if...else` conditions.

### Without Express routing

```
if (req.url === "/students" && req.method === "GET") {

    // Get all students

} else if (req.url === "/students" && req.method === "POST") {

    // Create student

} else if (req.url === "/students/1" && req.method === "DELETE") {

    // Delete student

}
```

### With Express routing

```
app.get("/students", (req, res) => {

    res.send("Get students");

});

app.post("/students", (req, res) => {

    res.send("Create student");

});

app.delete("/students/1", (req, res) => {

    res.send("Delete student");

});
```

### Advantages

- Easy to understand.
- Easy to maintain.
- Easy to organize.
- Easy to test using Postman.
- Easy to connect with databases.
- Easy to build REST APIs.

Express automatically matches the incoming HTTP method and URL with the correct route.

## 3. 🏢 Real-World Analogy

Imagine an Indian railway station.

A passenger wants to travel to a particular destination. Railway staff guide the passenger to the correct platform.

| Railway station    | Express.js     |
| ------------------ | -------------- |
| Passenger          | Client         |
| Destination        | URL path       |
| Journey request    | HTTP method    |
| Platform direction | Route matching |
| Platform staff     | Route handler  |

For example:

- One passenger wants to board a train from Platform 1.
- Another passenger wants to board from Platform 2.
- Staff direct each passenger to the correct platform.

Similarly, Express routing directs each HTTP request to the correct route handler.

## 4. 🔄 Architecture and Request Flow

Let's understand how a request travels from the client to Express.

### Visual flowchart

```
       CLIENT / POSTMAN
              |
              | HTTP REQUEST
              v
      +-------------------+
      |   EXPRESS SERVER  |
      |     server.js     |
      +-------------------+
              |
              v
      +-------------------+
      |   ROUTE MATCHING  |
      |                   |
      | HTTP Method + URL |
      +-------------------+
              |
              v
      +-------------------+
      |   ROUTE HANDLER   |
      |                   |
      | GET /students     |
      | POST /students    |
      | PUT /students/1   |
      | PATCH /students/1 |
      | DELETE /students/1|
      +-------------------+
              |
              v
      +-------------------+
      |   APPLICATION     |
      |      LOGIC        |
      |                   |
      | Read / Create     |
      | Update / Delete   |
      +-------------------+
              |
              v
      +-------------------+
      |   HTTP RESPONSE   |
      +-------------------+
              |
              v
            CLIENT
```

### Understand the flow

1. Client sends an HTTP request.
2. Express receives the request.
3. Express checks the HTTP method.
4. Express checks the URL path.
5. Matching route handler executes.
6. Handler performs the required operation.
7. Server sends a response.

## 5. 📝 HTTP Methods and Syntax

There are five important HTTP methods used in CRUD APIs.

Remember these five methods

### A. GET — Read data

Definition: GET is used to retrieve information from the server.

Example:

```
app.get("/students", (req, res) => {

    res.send("Getting all students");

});
```

Request:

```
GET http://localhost:3000/students
```

### B. POST — Create data

Definition: POST is used to submit data and usually create a new resource.

Example:

```
app.post("/students", (req, res) => {

    res.send("Student created successfully");

});
```

Request:

```
POST http://localhost:3000/students
```

### C. PUT — Replace data

Definition: PUT is generally used to replace the existing resource representation.

Example:

```
app.put("/students/:id", (req, res) => {

    res.send("Student replaced successfully");

});
```

Request:

```
PUT http://localhost:3000/students/1
```

### D. PATCH — Partially update data

Definition: PATCH is used to update only selected fields of an existing resource.

Example:

```
app.patch("/students/:id", (req, res) => {

    res.send("Student partially updated");

});
```

Request:

```
PATCH http://localhost:3000/students/1
```

### E. DELETE — Delete data

Definition: DELETE is used to request the deletion of a resource.

Example:

```
app.delete("/students/:id", (req, res) => {

    res.send("Student deleted successfully");

});
```

Request:

```
DELETE http://localhost:3000/students/1
```

### HTTP methods comparison

| Method | Operation      | Example       |
| ------ | -------------- | ------------- |
| GET    | Read           | `/students`   |
| POST   | Create         | `/students`   |
| PUT    | Replace        | `/students/1` |
| PATCH  | Partial update | `/students/1` |
| DELETE | Delete         | `/students/1` |

### Understand CRUD

CRUD means Create, Read, Update and Delete.

| CRUD   | HTTP method |
| ------ | ----------- |
| Create | POST        |
| Read   | GET         |
| Update | PUT / PATCH |
| Delete | DELETE      |

## 6. 💻 Basic Examples

Let's create a project and test each route.

### Step 1 — Create project folder

```
mkdir 18_Express_Routing

cd 18_Express_Routing
```

### Step 2 — Initialize Node.js project

```
npm init -y
```

### Step 3 — Install Express

```
npm install express
```

### Step 4 — Create a JavaScript file

```
18_Express_Routing/
│
├── package.json
├── package-lock.json
└── 01_get_route.js
```

### A. GET example

Create `01_get_route.js`.

```
// Import Express
const express = require("express");

// Create Express application
const app = express();

// GET route
app.get("/students", (req, res) => {

    // Send response to client
    res.send("Getting all students");

});

// Start server
app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Run:

```
node 01_get_route.js
```

Open this URL in your browser:

```
http://localhost:3000/students
```

Output:

```
Getting all students
```

A browser address bar normally sends a GET request. Use Postman for POST, PUT, PATCH and DELETE.

### B. POST example

Create `02_post_route.js`.

```
const express = require("express");

const app = express();

// POST route
app.post("/students", (req, res) => {

    res.send("Student created successfully");

});

app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Test using Postman:

```
Method: POST
URL: http://localhost:3000/students
```

Output:

```
Student created successfully
```

### C. PUT example

Create `03_put_route.js`.

```
const express = require("express");

const app = express();

// PUT route
app.put("/students/:id", (req, res) => {

    res.send("Student replaced successfully");

});

app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Request:

```
PUT http://localhost:3000/students/1
```

Output:

```
Student replaced successfully
```

### D. PATCH example

Create `04_patch_route.js`.

```
const express = require("express");

const app = express();

// PATCH route
app.patch("/students/:id", (req, res) => {

    res.send("Student partially updated");

});

app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Request:

```
PATCH http://localhost:3000/students/1
```

Output:

```
Student partially updated
```

### E. DELETE example

Create `05_delete_route.js`.

```
const express = require("express");

const app = express();

// DELETE route
app.delete("/students/:id", (req, res) => {

    res.send("Student deleted successfully");

});

app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Request:

```
DELETE http://localhost:3000/students/1
```

Output:

```
Student deleted successfully
```

Note: These five basic examples only send messages. They do not yet create, update or delete actual records. We will do that using raw data in Chapter 18's practical project below.

## 7. 🔍 Dry Run

Let's understand one GET request.

### Code

```
app.get("/students", (req, res) => {

    res.send("Student List");

});
```

### Client request

```
GET http://localhost:3000/students
```

### Execution steps

| Step | Action                   | Explanation            |
| ---- | ------------------------ | ---------------------- |
| 1    | Client sends request     | Requests `/students`   |
| 2    | Express receives request | Server receives it     |
| 3    | Express checks method    | Checks GET             |
| 4    | Express checks path      | Checks `/students`     |
| 5    | Handler executes         | Callback function runs |
| 6    | `res.send()` executes    | Sends response         |
| 7    | Client receives response | Displays Student List  |

### Visual dry run

```
GET /students
      |
      v
Express Server
      |
      v
Check HTTP Method
      |
      v
Check URL Path
      |
      v
Find Matching GET Route
      |
      v
Execute Callback Function
      |
      v
res.send("Student List")
      |
      v
Client receives response
```

Important: Express checks both the HTTP method and the URL path.

For example, a POST request to `/students` will not match a GET route for `/students`.

## 8. 📤 Expected Outputs

| Request              | Expected output               |
| -------------------- | ----------------------------- |
| GET `/students`      | Getting all students          |
| POST `/students`     | Student created successfully  |
| PUT `/students/1`    | Student replaced successfully |
| PATCH `/students/1`  | Student partially updated     |
| DELETE `/students/1` | Student deleted successfully  |

These are example messages. Real CRUD routes will return actual data, which we will learn below.

## 9. 📦 Request Data: params, query, body

This is one of the most important sections in Express Routing.

When a client sends a request, it can send data in different places.

Express provides three important properties:

1. `req.params`
2. `req.query`
3. `req.body`

Let's understand each one with raw examples.

### A. Route parameters — `req.params`

Definition: Route parameters are dynamic values included directly in the URL path.

Example URL:

```
http://localhost:3000/students/101
```

Here:

- `students` is the resource.
- `101` is the student ID.

How do we read `101`?

```
app.get("/students/:id", (req, res) => {

    const id = req.params.id;

    res.send(`Student ID: ${id}`);

});
```

Output:

```
Student ID: 101
```

The `:id` syntax creates a dynamic route parameter.

#### Understand the raw value

```
const id = req.params.id;

console.log(id);
```

Output:

```
101
```

Important: Route parameter values are strings by default.

If you need a number:

```
const id = Number(req.params.id);

console.log(id);
```

Now `id` is the number `101`.

#### Multiple route parameters

URL:

```
/students/101/courses/501
```

Code:

```
app.get("/students/:studentId/courses/:courseId", (req, res) => {

    const studentId = req.params.studentId;

    const courseId = req.params.courseId;

    res.json({
        studentId: studentId,
        courseId: courseId
    });

});
```

Output:

```
{
    "studentId": "101",
    "courseId": "501"
}
```

### B. Query parameters — `req.query`

Definition: Query parameters are additional values sent after the `?` symbol in a URL.

Example:

```
http://localhost:3000/students?name=Ramesh
```

Here:

| Part     | Value                   |
| -------- | ----------------------- |
| `?`      | Starts query parameters |
| `name`   | Query key               |
| `Ramesh` | Query value             |

Code:

```
app.get("/students", (req, res) => {

    const name = req.query.name;

    res.send(`Student Name: ${name}`);

});
```

Output:

```
Student Name: Ramesh
```

#### Multiple query parameters

URL:

```
/students?name=Ramesh&course=Node.js
```

Code:

```
app.get("/students", (req, res) => {

    const name = req.query.name;

    const course = req.query.course;

    res.json({
        name: name,
        course: course
    });

});
```

Output:

```
{
    "name": "Ramesh",
    "course": "Node.js"
}
```

#### Real-world query parameter examples

| Purpose    | Example URL                 |
| ---------- | --------------------------- |
| Search     | `/students?name=Ramesh`     |
| Filter     | `/students?course=Node.js`  |
| Pagination | `/students?page=1&limit=10` |
| Sorting    | `/students?sort=name`       |

Use query parameters for searching, filtering, sorting and pagination.

### C. Request body — `req.body`

Definition: The request body contains data sent by the client to the server.

Imagine a student registration form.

The user enters:

- Name: Ramesh
- Course: Node.js
- Age: 25

The frontend sends this data to the backend.

Raw JSON data:

```
{
    "name": "Ramesh",
    "course": "Node.js",
    "age": 25
}
```

How do we read this data in Express?

First, add:

```
app.use(express.json());
```

Then:

```
app.post("/students", (req, res) => {

    const student = req.body;

    console.log(student);

    res.json(student);

});
```

Output:

```
{
    "name": "Ramesh",
    "course": "Node.js",
    "age": 25
}
```

### Understand `req.body` step by step

```
const student = req.body;
```

Suppose the client sends:

```
{
    "name": "Ramesh",
    "course": "Node.js"
}
```

Then:

```
student.name
```

Output:

```
Ramesh
```

And:

```
student.course
```

Output:

```
Node.js
```

Remember: `express.json()` parses incoming JSON request bodies so that Express can provide the parsed data through `req.body`.

### D. Difference between params, query and body

| Property     | Where data comes from | Example                 |
| ------------ | --------------------- | ----------------------- |
| `req.params` | URL path              | `/students/101`         |
| `req.query`  | URL query string      | `/students?name=Ramesh` |
| `req.body`   | Request body          | `{ "name": "Ramesh" }`  |

### E. Route handlers and `next()`

Definition: A route handler is a function that executes when an incoming request matches a route.

Example:

```
app.get("/students", (req, res) => {

    res.send("Student List");

});
```

Here, the arrow function is the route handler.

Express also supports multiple handlers for one route.

```
app.get(
    "/students",

    (req, res, next) => {

        console.log("First handler");

        next();

    },

    (req, res) => {

        res.send("Student List");

    }

);
```

Execution:

1. First handler runs.
2. `next()` passes control to the next handler.
3. Second handler sends the response.

Terminal output:

```
First handler
```

Browser output:

```
Student List
```

If a handler neither sends a response nor calls `next()`, the request may remain unfinished.

## 10. 🏗️ Practical Project — Student CRUD API Using Raw Data

Now let's build a complete Student Management API.

This is the most important practical example in this chapter.

We will use a JavaScript array as our temporary data storage instead of a database.

### 10.1 What is raw data?

Raw data means the actual values stored in your program.

Example:

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

Let's understand this data.

### Data structure

```
students
   |
   v
+--------------------------+
|        ARRAY             |
|                          |
|  Index 0                 |
|  {                       |
|    id: 1,                |
|    name: "Ramesh",       |
|    course: "Node.js",    |
|    age: 25               |
|  }                       |
|                          |
|  Index 1                 |
|  {                       |
|    id: 2,                |
|    name: "Kumar",        |
|    course: "React.js",   |
|    age: 24               |
|  }                       |
|                          |
|  Index 2                 |
|  {                       |
|    id: 3,                |
|    name: "Suresh",       |
|    course: "Python",     |
|    age: 26               |
|  }                       |
+--------------------------+
```

### Understand the raw data

| Index | ID | Name   | Course   | Age |
| ----- | -- | ------ | -------- | --- |
| 0     | 1  | Ramesh | Node.js  | 25  |
| 1     | 2  | Kumar  | React.js | 24  |
| 2     | 3  | Suresh | Python   | 26  |

Important JavaScript concepts:

| Code       | Meaning         |
| ---------- | --------------- |
| `students` | Array variable  |
| `[]`       | Array           |
| `{}`       | Object          |
| `id`       | Object property |
| `"Ramesh"` | String value    |
| `25`       | Number value    |

### 10.2 How will CRUD work with this array?

| Operation | JavaScript method  | Purpose                |
| --------- | ------------------ | ---------------------- |
| GET       | `map()` / `find()` | Read records           |
| POST      | `push()`           | Add new record         |
| PUT       | Direct assignment  | Replace record         |
| PATCH     | Update properties  | Change selected fields |
| DELETE    | `splice()`         | Remove record          |

Let's understand each operation with raw data.

### 10.3 GET — Read all students

Requirement: Return all student records.

Raw data:

```
let students = [
    { id: 1, name: "Ramesh", course: "Node.js" },
    { id: 2, name: "Kumar", course: "React.js" },
    { id: 3, name: "Suresh", course: "Python" }
];
```

Route:

```
app.get("/students", (req, res) => {

    res.json(students);

});
```

Output:

```
[
    {
        "id": 1,
        "name": "Ramesh",
        "course": "Node.js"
    },
    {
        "id": 2,
        "name": "Kumar",
        "course": "React.js"
    },
    {
        "id": 3,
        "name": "Suresh",
        "course": "Python"
    }
]
```

`res.json(students)` sends the entire array as a JSON response.

### 10.4 GET — Read one student by ID

Requirement: Find the student whose ID is 2.

Raw data:

```
let students = [
    { id: 1, name: "Ramesh", course: "Node.js" },
    { id: 2, name: "Kumar", course: "React.js" },
    { id: 3, name: "Suresh", course: "Python" }
];
```

Request:

```
GET /students/2
```

Code:

```
app.get("/students/:id", (req, res) => {

    // Read ID from URL
    const id = Number(req.params.id);

    // Find student using ID
    const student = students.find((item) => item.id === id);

    // Check if student exists
    if (!student) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    // Send student data
    res.json(student);

});
```

### Understand `.find()`

```
const student = students.find((item) => item.id === 2);
```

Dry run:

| Student      | Condition `item.id === 2` | Result            |
| ------------ | ------------------------- | ----------------- |
| Ramesh, ID 1 | `1 === 2`                 | False             |
| Kumar, ID 2  | `2 === 2`                 | True              |
| Suresh, ID 3 | Not checked               | Stops after match |

Output:

```
{
    "id": 2,
    "name": "Kumar",
    "course": "React.js"
}
```

The `.find()` method returns the first matching element. If nothing matches, it returns `undefined`.

### 10.5 POST — Create a new student

Requirement: Receive student data and add it to the array.

Client sends this raw JSON data:

```
{
    "name": "Praveen",
    "course": "FastAPI",
    "age": 27
}
```

Code:

```
app.post("/students", (req, res) => {

    // Read data from request body
    const { name, course, age } = req.body;

    // Check required fields
    if (!name || !course || age === undefined) {

        return res.status(400).json({
            message: "Name, course and age are required"
        });

    }

    // Create a new student object
    const newStudent = {
        id: students.length
            ? Math.max(...students.map(student => student.id)) + 1
            : 1,
        name: name,
        course: course,
        age: age
    };

    // Add object to array
    students.push(newStudent);

    // Send response
    res.status(201).json({
        message: "Student created successfully",
        data: newStudent
    });

});
```

### Understand `.push()`

Before POST:

```
[
    { id: 1, name: "Ramesh" },
    { id: 2, name: "Kumar" },
    { id: 3, name: "Suresh" }
]
```

Client sends:

```
{
    "name": "Praveen",
    "course": "FastAPI",
    "age": 27
}
```

After POST:

```
[
    { id: 1, name: "Ramesh" },
    { id: 2, name: "Kumar" },
    { id: 3, name: "Suresh" },
    { id: 4, name: "Praveen", course: "FastAPI", age: 27 }
]
```

`.push()` adds a new item to the end of an array.

Expected response:

```
{
    "message": "Student created successfully",
    "data": {
        "id": 4,
        "name": "Praveen",
        "course": "FastAPI",
        "age": 27
    }
}
```

### 10.6 PUT — Replace student data

Requirement: Replace all student details for ID 2.

Request:

```
PUT /students/2
```

Client sends:

```
{
    "name": "Kumar Updated",
    "course": "Node.js",
    "age": 28
}
```

Code:

```
app.put("/students/:id", (req, res) => {

    // Get ID from URL
    const id = Number(req.params.id);

    // Get new data from request body
    const { name, course, age } = req.body;

    // Find student position
    const index = students.findIndex((item) => item.id === id);

    // Check if student exists
    if (index === -1) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    // Validate all required fields
    if (!name || !course || age === undefined) {

        return res.status(400).json({
            message: "Name, course and age are required"
        });

    }

    // Replace the entire object
    students[index] = {
        id: id,
        name: name,
        course: course,
        age: age
    };

    res.json({
        message: "Student replaced successfully",
        data: students[index]
    });

});
```

### Understand `.findIndex()`

```
const index = students.findIndex((item) => item.id === 2);
```

Output:

```
1
```

Why?

Because arrays start counting from index `0`.

| Index | Student ID | Name   |
| ----- | ---------- | ------ |
| 0     | 1          | Ramesh |
| 1     | 2          | Kumar  |
| 2     | 3          | Suresh |

So the student with ID 2 is at index 1.

Before PUT:

```
{
    id: 2,
    name: "Kumar",
    course: "React.js",
    age: 24
}
```

After PUT:

```
{
    id: 2,
    name: "Kumar Updated",
    course: "Node.js",
    age: 28
}
```

PUT replaces the resource representation with the submitted data.

### 10.7 PATCH — Update only selected fields

Requirement: Update only the course of student ID 2.

Request:

```
PATCH /students/2
```

Client sends:

```
{
    "course": "FastAPI"
}
```

Code:

```
app.patch("/students/:id", (req, res) => {

    // Get student ID
    const id = Number(req.params.id);

    // Find student
    const student = students.find((item) => item.id === id);

    // Check student exists
    if (!student) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    // Read fields from request body
    const { name, course, age } = req.body;

    // Update only provided fields
    if (name !== undefined) {
        student.name = name;
    }

    if (course !== undefined) {
        student.course = course;
    }

    if (age !== undefined) {
        student.age = age;
    }

    res.json({
        message: "Student updated successfully",
        data: student
    });

});
```

### Understand PATCH with raw data

Before PATCH:

```
{
    id: 2,
    name: "Kumar",
    course: "React.js",
    age: 24
}
```

Client sends:

```
{
    "course": "FastAPI"
}
```

After PATCH:

```
{
    id: 2,
    name: "Kumar",
    course: "FastAPI",
    age: 24
}
```

What changed?

| Field  | Before   | After   |
| ------ | -------- | ------- |
| id     | 2        | 2       |
| name   | Kumar    | Kumar   |
| course | React.js | FastAPI |
| age    | 24       | 24      |

PATCH changes only the fields supplied by the client.

### 10.8 DELETE — Delete student

Requirement: Delete student ID 2.

Request:

```
DELETE /students/2
```

Code:

```
app.delete("/students/:id", (req, res) => {

    // Get ID from URL
    const id = Number(req.params.id);

    // Find student position
    const index = students.findIndex((item) => item.id === id);

    // Check student exists
    if (index === -1) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    // Remove student from array
    const deletedStudent = students.splice(index, 1)[0];

    res.json({
        message: "Student deleted successfully",
        data: deletedStudent
    });

});
```

### Understand `.splice()`

Before DELETE:

```
[
    { id: 1, name: "Ramesh" },
    { id: 2, name: "Kumar" },
    { id: 3, name: "Suresh" }
]
```

We execute:

```
students.splice(1, 1);
```

Meaning:

- First `1` = Start at index 1.
- Second `1` = Remove one element.

After DELETE:

```
[
    { id: 1, name: "Ramesh" },
    { id: 3, name: "Suresh" }
]
```

`.splice()` can remove elements from an array and changes the original array.

### 10.9 Search students using query parameters

Requirement: Get only students from the Node.js course.

Request:

```
GET /students?course=Node.js
```

Code:

```
app.get("/students", (req, res) => {

    // Read course from query parameter
    const course = req.query.course;

    // If course is not provided, return all students
    if (!course) {

        return res.json(students);

    }

    // Filter students by course
    const result = students.filter((student) =>
        student.course.toLowerCase() === course.toLowerCase()
    );

    res.json(result);

});
```

### Understand `.filter()`

Raw data:

```
let students = [
    { id: 1, name: "Ramesh", course: "Node.js" },
    { id: 2, name: "Kumar", course: "React.js" },
    { id: 3, name: "Suresh", course: "Node.js" }
];
```

Request:

```
GET /students?course=Node.js
```

Output:

```
[
    {
        "id": 1,
        "name": "Ramesh",
        "course": "Node.js"
    },
    {
        "id": 3,
        "name": "Suresh",
        "course": "Node.js"
    }
]
```

`.filter()` returns a new array containing all elements that satisfy the condition.

### 10.10 Complete Student CRUD API

Now combine everything into one file.

Create `10_student_routes.js`.

```
// ======================================
// 1. IMPORT EXPRESS
// ======================================

const express = require("express");

// Create Express application
const app = express();

const PORT = 3000;


// ======================================
// 2. MIDDLEWARE
// ======================================

// Parse incoming JSON request bodies
app.use(express.json());


// ======================================
// 3. RAW STUDENT DATA
// ======================================

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


// ======================================
// 4. GET - ALL STUDENTS
// ======================================

app.get("/students", (req, res) => {

    const course = req.query.course;

    // If course is provided, filter the data
    if (course) {

        const result = students.filter((student) =>
            student.course.toLowerCase() === course.toLowerCase()
        );

        return res.status(200).json(result);

    }

    // Otherwise return all students
    res.status(200).json(students);

});


// ======================================
// 5. GET - STUDENT BY ID
// ======================================

app.get("/students/:id", (req, res) => {

    const id = Number(req.params.id);

    const student = students.find((item) => item.id === id);

    if (!student) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    res.status(200).json(student);

});


// ======================================
// 6. POST - CREATE STUDENT
// ======================================

app.post("/students", (req, res) => {

    const { name, course, age } = req.body;

    if (!name || !course || age === undefined) {

        return res.status(400).json({
            message: "Name, course and age are required"
        });

    }

    const newStudent = {

        id: students.length
            ? Math.max(...students.map(student => student.id)) + 1
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


// ======================================
// 7. PUT - REPLACE STUDENT
// ======================================

app.put("/students/:id", (req, res) => {

    const id = Number(req.params.id);

    const { name, course, age } = req.body;

    const index = students.findIndex((item) => item.id === id);

    if (index === -1) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

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
        message: "Student replaced successfully",
        data: students[index]
    });

});


// ======================================
// 8. PATCH - PARTIALLY UPDATE STUDENT
// ======================================

app.patch("/students/:id", (req, res) => {

    const id = Number(req.params.id);

    const student = students.find((item) => item.id === id);

    if (!student) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    const { name, course, age } = req.body;

    if (name !== undefined) {
        student.name = name;
    }

    if (course !== undefined) {
        student.course = course;
    }

    if (age !== undefined) {
        student.age = age;
    }

    res.status(200).json({
        message: "Student updated successfully",
        data: student
    });

});


// ======================================
// 9. DELETE - STUDENT
// ======================================

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


// ======================================
// 10. START SERVER
// ======================================

app.listen(PORT, () => {

    console.log(`Student API running on port ${PORT}`);

});
```

### 10.11 Run the project

```
node 10_student_routes.js
```

Terminal:

```
Student API running on port 3000
```

### 10.12 Test all endpoints using Postman

| Method | URL                                             | Purpose                |
| ------ | ----------------------------------------------- | ---------------------- |
| GET    | `http://localhost:3000/students`                | Get all students       |
| GET    | `http://localhost:3000/students/1`              | Get student by ID      |
| GET    | `http://localhost:3000/students?course=Node.js` | Filter by course       |
| POST   | `http://localhost:3000/students`                | Create student         |
| PUT    | `http://localhost:3000/students/1`              | Replace student        |
| PATCH  | `http://localhost:3000/students/1`              | Update selected fields |
| DELETE | `http://localhost:3000/students/1`              | Delete student         |

### Postman — How to send POST data

1. Open Postman.
2. Select the POST method.
3. Enter `http://localhost:3000/students`.
4. Click Body.
5. Select raw.
6. Select JSON.
7. Enter the data.

Raw JSON:

```
{
    "name": "Praveen",
    "course": "FastAPI",
    "age": 27
}
```

Click Send.

### Postman — How to send PATCH data

Select PATCH:

```
http://localhost:3000/students/1
```

Body → raw → JSON:

```
{
    "course": "Express.js"
}
```

Click Send.

### Important: What happens to the raw data?

- GET reads the array.
- POST adds an object to the array.
- PUT replaces an object.
- PATCH changes selected object properties.
- DELETE removes an object from the array.

The array is temporary storage. When you restart the Node.js server, the original data returns. Later, we will use MongoDB to store data permanently.

## 11. ⚠️ Common Mistakes

### Mistake 1 — Forgetting `express.json()`

Incorrect:

```
const app = express();

app.post("/students", (req, res) => {

    console.log(req.body);

});
```

Correct:

```
const app = express();

app.use(express.json());

app.post("/students", (req, res) => {

    console.log(req.body);

    res.json(req.body);

});
```

Without JSON parsing middleware, `req.body` will generally be undefined for incoming JSON requests.

### Mistake 2 — Using `req.params` for query parameters

URL:

```
/students?name=Ramesh
```

Incorrect:

```
const name = req.params.name;
```

Correct:

```
const name = req.query.name;
```

### Mistake 3 — Using `req.query` for route parameters

URL:

```
/students/101
```

Correct:

```
const id = req.params.id;
```

### Mistake 4 — Forgetting to convert ID into a number

```
const id = req.params.id;
```

This gives a string.

If your array stores numeric IDs, use:

```
const id = Number(req.params.id);
```

### Mistake 5 — Forgetting `return` after an error response

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

Using `return` prevents the function from continuing after sending the error response.

### Mistake 6 — Confusing PUT and PATCH

| PUT                                  | PATCH                        |
| ------------------------------------ | ---------------------------- |
| Replaces resource representation     | Partially updates resource   |
| Usually sends all required fields    | Can send only changed fields |
| Example: replace all student details | Example: change only course  |

### Mistake 7 — Forgetting to send a response

Incorrect:

```
app.get("/students", (req, res) => {

    const students = [];

});
```

Correct:

```
app.get("/students", (req, res) => {

    const students = [];

    res.json(students);

});
```

## 12. ✅ Best Practices

1. Use meaningful resource-based URLs.
2. Use the correct HTTP methods.
3. Use route parameters to identify resources.
4. Use query parameters for searching and filtering.
5. Use the request body for submitted data.
6. Validate incoming data.
7. Return appropriate HTTP status codes.
8. Use `express.json()` for JSON request bodies.
9. Use `return` after sending an early error response.
10. Keep route handlers readable.
11. Avoid putting all routes in one large file as your project grows.
12. Do not trust client input without validation.

### Professional route naming

Good:

```
GET    /api/students
GET    /api/students/101
POST   /api/students
PUT    /api/students/101
PATCH  /api/students/101
DELETE /api/students/101
```

Avoid inconsistent endpoint names:

```
GET  /getAllStudents
POST /createNewStudent
```

### Recommended folder structure

For this chapter, you can organize your learning files like this:

```
18_Express_Routing/
│
├── README.md
│
├── 01_get_route.js
├── 02_post_route.js
├── 03_put_route.js
├── 04_patch_route.js
├── 05_delete_route.js
│
├── 06_route_params.js
├── 07_query_params.js
├── 08_request_body.js
├── 09_route_handlers.js
│
├── 10_student_routes.js
│
└── 11_employee_challenge.js
```

No images or Mermaid diagrams are needed. The text flowcharts and code examples are enough for your GitHub README.

## 13. 🎯 Interview Questions

### Beginner Level

### Intermediate Level

### Advanced Level

## 14. 📝 Practice Problems

Try these exercises in VS Code.

### Beginner Level

- Exercise 1: Create `GET /employees` to return all employees.
- Exercise 2: Create `POST /employees` to receive employee information.
- Exercise 3: Create `GET /employees/:id` to read an employee ID.
- Exercise 4: Create `GET /products?category=mobile` to read the category.

### Intermediate Level

- Exercise 5: Create `PUT /employees/:id` to replace employee details.
- Exercise 6: Create `PATCH /employees/:id` to update only the employee email.
- Exercise 7: Create `DELETE /employees/:id` to delete an employee.

### Advanced Level

- Exercise 8: Create a route with two parameters: `/orders/:orderId/items/:itemId`.
- Exercise 9: Create a route to filter employees by department.
- Exercise 10: Build a complete CRUD API using an array of employee objects.

## 15. 🏆 Mini Challenge — Employee Management API

Practical Challenge

Requirement: Build an Employee Management API using Express Routing and raw JavaScript data.

### Step 1 — Sample raw data

Start with this array:

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
        department: "IT",
        salary: 35000
    }

];
```

### Step 2 — Required endpoints

| Method | Endpoint                   | Operation                 |
| ------ | -------------------------- | ------------------------- |
| GET    | `/employees`               | Get all employees         |
| GET    | `/employees/:id`           | Get employee by ID        |
| GET    | `/employees?department=IT` | Filter by department      |
| POST   | `/employees`               | Create employee           |
| PUT    | `/employees/:id`           | Replace employee          |
| PATCH  | `/employees/:id`           | Update employee partially |
| DELETE | `/employees/:id`           | Delete employee           |

### Step 3 — Starter code

Create `11_employee_challenge.js`.

```
const express = require("express");

const app = express();

app.use(express.json());

const PORT = 3000;

// Sample employees
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
        department: "IT",
        salary: 35000
    }
];

// 1. GET all employees


// 2. GET employee by ID


// 3. Filter employees by department


// 4. POST new employee


// 5. PUT employee


// 6. PATCH employee


// 7. DELETE employee


// Start server
app.listen(PORT, () => {

    console.log(`Employee API running on port ${PORT}`);

});
```

### Step 4 — Expected output

For this request:

```
GET http://localhost:3000/employees?department=IT
```

Expected response:

```
[
    {
        "id": 1,
        "name": "Ramesh",
        "department": "IT",
        "salary": 30000
    },
    {
        "id": 3,
        "name": "Suresh",
        "department": "IT",
        "salary": 35000
    }
]
```

### Step 5 — Build the logic step by step

For every coding problem, follow this sequence:

1. Requirement: What should the API do?
2. Input: What data will the client send?
3. Output: What response should the server return?
4. Steps: Break the requirement into small steps.
5. Hint: Identify the JavaScript method you need.
6. Pseudocode: Write the logic in simple English.
7. Try: Write the code yourself.
8. Review: Check the result.
9. Correct: Fix errors.
10. Dry run: Check how the data changes.
11. Improve: Add validation and error responses.

Try this challenge yourself first. Send me your code, and I will explain it line by line.

## 16. 📌 Chapter Summary

| Topic            | What you learned                |
| ---------------- | ------------------------------- |
| Express Routing  | Matching requests to handlers   |
| `app.get()`      | Retrieve information            |
| `app.post()`     | Create a resource               |
| `app.put()`      | Replace a resource              |
| `app.patch()`    | Partially update a resource     |
| `app.delete()`   | Delete a resource               |
| `req.params`     | Read route parameters           |
| `req.query`      | Read query parameters           |
| `req.body`       | Read request body               |
| `express.json()` | Parse JSON request bodies       |
| `res.send()`     | Send a response                 |
| `res.json()`     | Send a JSON response            |
| `res.status()`   | Set HTTP status code            |
| `.find()`        | Find one matching item          |
| `.findIndex()`   | Find the position of an item    |
| `.filter()`      | Filter matching items           |
| `.push()`        | Add an item                     |
| `.splice()`      | Remove an item                  |
| `next()`         | Pass control to another handler |

Most important takeaway: Express Routing connects an HTTP method and URL to the function that performs the required operation.

## 17. ⚡ Quick Revision

### 1. Important HTTP methods

```
GET     = READ
POST    = CREATE
PUT     = REPLACE
PATCH   = PARTIAL UPDATE
DELETE  = DELETE
```

### 2. Important request properties

| Property     | Example                 |
| ------------ | ----------------------- |
| `req.params` | `/students/101`         |
| `req.query`  | `/students?name=Ramesh` |
| `req.body`   | `{ "name": "Ramesh" }`  |

### 3. Important JavaScript array methods

```
// Read one student
students.find(student => student.id === 1);

// Find student position
students.findIndex(student => student.id === 1);

// Filter students
students.filter(student => student.course === "Node.js");

// Add student
students.push(newStudent);

// Remove student
students.splice(index, 1);
```

### 4. Quick memory flow

```
CLIENT
  |
  v
HTTP REQUEST
  |
  v
EXPRESS SERVER
  |
  v
MATCH METHOD + URL
  |
  v
ROUTE HANDLER
  |
  v
READ / CREATE / UPDATE / DELETE
  |
  v
HTTP RESPONSE
  |
  v
CLIENT
```

### 5. Final checklist

- I understand Express Routing.
- I understand all five HTTP methods.
- I can create GET and POST routes.
- I can create PUT, PATCH and DELETE routes.
- I understand `req.params`.
- I understand `req.query`.
- I understand `req.body`.
- I understand `express.json()`.
- I understand raw JavaScript array data.
- I can use `find()`, `filter()`, `push()` and `splice()`.
- I can build a simple CRUD API.
- I can test API endpoints using Postman.

Chapter 18 completed

Before moving forward, practise the Employee Management API. Focus especially on understanding how raw data changes when you use POST, PUT, PATCH and DELETE.

Next chapter:

# Chapter 19 — Express Middleware

You will learn:

1. What is middleware?
2. Request lifecycle.
3. `req`, `res`, `next`.
4. Application middleware.
5. Router middleware.
6. Built-in middleware.
7. Third-party middleware.
8. Error middleware.
9. Custom middleware.
10. Logger, authentication and validation middleware.

Type `NEXT` when you are ready.