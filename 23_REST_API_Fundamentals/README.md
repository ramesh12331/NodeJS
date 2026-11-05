# 🚀 PART 6 — REST API DEVELOPMENT

# Chapter 23 — Introduction to REST API

BEGINNER LEVEL → PRACTICAL LEVEL

## 📚 Table of Contents

1. What is an API?
2. What is REST?
3. What is a REST API?
4. Why do we need REST APIs?
5. Real-world Analogy
6. Client-Server Architecture
7. HTTP Methods
8. HTTP Request and Response
9. JSON Data Format
10. REST Principles
11. Resource-Based URLs
12. Practical Example — Student REST API
13. Common Mistakes
14. Best Practices
15. Interview Questions
16. Practice Problems
17. Mini Challenge
18. Chapter Summary & Quick Revision

## 1. 🧠 What is an API?

API stands for Application Programming Interface.

An API allows two software applications to communicate with each other.

In simple words:

Imagine you have a React frontend and a Node.js backend.

- React needs student data.
- Node.js stores or retrieves student data.
- React sends a request to Node.js.
- Node.js sends a response to React.

The API acts as the communication point between them.

### Simple example

You have a React application displaying students.

React sends:

```
GET /api/students
```

Node.js responds:

```
{
    "message": "Students fetched successfully",
    "data": [
        {
            "id": 1,
            "name": "Ramesh",
            "course": "Node.js"
        },
        {
            "id": 2,
            "name": "Kumar",
            "course": "React.js"
        }
    ]
}
```

React receives this JSON data and displays it on the screen.

## 2. 🔍 What is REST?

REST stands for Representational State Transfer.

REST is an architectural style used to design network-based APIs.

It provides guidelines for designing APIs in a consistent way.

REST commonly uses:

- HTTP methods
- Resource-based URLs
- JSON request and response data
- HTTP status codes
- Stateless communication

### Example

Consider a Student Management API.

```
GET     /students
POST    /students
GET     /students/1
PUT     /students/1
PATCH   /students/1
DELETE  /students/1
```

Each URL represents a resource, and the HTTP method describes the operation.

## 3. 🚀 What is a REST API?

A REST API is an API designed using REST architectural principles.

It allows applications to communicate using HTTP requests and responses.

### Example

Suppose we have a Student Management System.

| Operation        | HTTP Method | URL               |
| ---------------- | ----------- | ----------------- |
| Get all students | GET         | `/api/students`   |
| Get one student  | GET         | `/api/students/1` |
| Create student   | POST        | `/api/students`   |
| Update student   | PUT         | `/api/students/1` |
| Partially update | PATCH       | `/api/students/1` |
| Delete student   | DELETE      | `/api/students/1` |

### Remember

- API: Communication interface between applications.
- REST: Architectural style for designing APIs.
- REST API: API designed according to REST principles.

## 4. 🤔 Why do we need REST APIs?

Imagine you are developing an application with:

- React frontend
- Node.js backend
- MongoDB database

How will React communicate with Node.js?

How will Node.js send information back to React?

We use APIs.

### Without API communication

```
React Frontend

    X

Node.js Backend
```

The applications do not have an established communication interface.

### With API communication

```
REACT FRONTEND
      |
      | HTTP Request
      v
NODE.JS REST API
      |
      v
MONGODB DATABASE
      |
      v
NODE.JS REST API
      |
      | JSON Response
      v
REACT FRONTEND
```

### Benefits of REST APIs

1. Frontend and backend can be developed separately.
2. Different applications can use the same API.
3. APIs can return structured JSON data.
4. Applications can communicate over HTTP.
5. APIs can be organized around resources.
6. Easier integration with mobile applications.

## 5. 🌍 Real-world Analogy

Imagine ordering food in a restaurant.

```
CUSTOMER
   |
   | Places Order
   v
WAITER
   |
   | Sends Order
   v
KITCHEN
   |
   | Prepares Food
   v
WAITER
   |
   | Delivers Food
   v
CUSTOMER
```

In this example:

| Restaurant | API           |
| ---------- | ------------- |
| Customer   | Client        |
| Waiter     | API interface |
| Kitchen    | Backend       |
| Food       | Response data |
| Order      | Request       |

The customer does not directly enter the kitchen. The waiter handles communication.

Similarly, a frontend application communicates with the backend through an API.

## 6. 🏗️ Client-Server Architecture

Client-server architecture is a model in which a client sends requests and a server processes them.

### Client

The client is the application that sends a request.

Examples:

- React application
- Mobile application
- Web browser
- Postman

### Server

The server receives the request, performs operations and sends a response.

Examples:

- Node.js
- Express.js
- Python FastAPI
- Django

### Architecture

```
+-------------------------+
|         CLIENT          |
|                         |
|      React App          |
+-------------------------+
            |
            | HTTP Request
            v
+-------------------------+
|         SERVER          |
|                         |
|     Node.js + Express   |
+-------------------------+
            |
            v
+-------------------------+
|        DATABASE         |
|                         |
|        MongoDB          |
+-------------------------+
```

### Example request flow

1. User opens the student page.
2. React sends a GET request.
3. Express receives the request.
4. Backend retrieves student data.
5. Backend sends JSON response.
6. React displays the students.

## 7. 🌐 HTTP Methods

HTTP methods describe what operation the client wants to perform.

These are the most commonly used methods in REST APIs.

### 1. GET — Read Data

Used to retrieve data.

```
GET /api/students
```

Example response:

```
{
    "id": 1,
    "name": "Ramesh",
    "course": "Node.js"
}
```

### 2. POST — Create Data

Used to create a new resource.

```
POST /api/students
```

Request body:

```
{
    "name": "Anil",
    "course": "FastAPI",
    "age": 23
}
```

### 3. PUT — Replace Data

Used to replace an existing resource.

```
PUT /api/students/1
```

Request body:

```
{
    "name": "Ramesh Kumar",
    "course": "Full Stack",
    "age": 26
}
```

### 4. PATCH — Partially Update Data

Used to update selected fields.

```
PATCH /api/students/1
```

Request body:

```
{
    "course": "Machine Learning"
}
```

### 5. DELETE — Delete Data

Used to remove a resource.

```
DELETE /api/students/1
```

### Quick revision

| Method | Operation      | Example                 |
| ------ | -------------- | ----------------------- |
| GET    | Read           | Get students            |
| POST   | Create         | Add student             |
| PUT    | Replace        | Replace student details |
| PATCH  | Partial update | Update course           |
| DELETE | Delete         | Remove student          |

## 8. 🔄 HTTP Request and Response

Let's understand how requests and responses work.

### What is an HTTP Request?

An HTTP request is a message sent by a client to a server.

A request can contain:

- HTTP method
- URL
- Headers
- Body

Example:

```
POST /api/students HTTP/1.1
Content-Type: application/json
```

Request body:

```
{
    "name": "Anil",
    "course": "FastAPI",
    "age": 23
}
```

### What is an HTTP Response?

An HTTP response is a message sent by the server back to the client.

A response contains:

- Status code
- Headers
- Body

Example:

```
HTTP/1.1 201 Created
Content-Type: application/json
```

Response body:

```
{
    "message": "Student created successfully",
    "data": {
        "id": 4,
        "name": "Anil",
        "course": "FastAPI",
        "age": 23
    }
}
```

### Request-response flow

```
CLIENT
  |
  | POST /api/students
  | JSON Request Body
  v
EXPRESS SERVER
  |
  | Validate Request
  | Create Student
  v
JSON RESPONSE
  |
  v
CLIENT
```

## 9. 📦 JSON Data Format

JSON stands for JavaScript Object Notation.

JSON is a lightweight data format used to exchange data between applications.

### JavaScript object

```
const student = {
    id: 1,
    name: "Ramesh",
    course: "Node.js",
    age: 25
};
```

### Equivalent JSON

```
{
    "id": 1,
    "name": "Ramesh",
    "course": "Node.js",
    "age": 25
}
```

### JavaScript object vs JSON

| JavaScript Object              | JSON                                                          |
| ------------------------------ | ------------------------------------------------------------- |
| Used in JavaScript code        | Used as a data exchange format                                |
| Keys can be unquoted           | Keys must use double quotes                                   |
| Can contain functions          | Cannot contain functions                                      |
| Can contain `undefined`        | No `undefined` value                                          |
| Supports more JavaScript types | Supports strings, numbers, booleans, null, arrays and objects |

### JSON array example

```
[
    {
        "id": 1,
        "name": "Ramesh"
    },
    {
        "id": 2,
        "name": "Kumar"
    },
    {
        "id": 3,
        "name": "Suresh"
    }
]
```

### Reading JSON in Express

```
app.use(express.json());
```

This middleware parses incoming JSON request bodies and makes the parsed data available through `req.body`.

Example:

```
app.post("/students", (req, res) => {

    console.log(req.body);

    res.json({
        message: "Data received",
        data: req.body
    });

});
```

## 10. 📐 REST Principles

REST APIs are designed using a set of architectural constraints.

Here are the six main REST constraints.

### 1. Client-Server

Client and server have separate responsibilities.

```
React Client  --->  Express Server
```

The frontend handles the user interface. The backend handles application logic and data.

### 2. Stateless

Each request should contain the information needed to process it.

The server should not depend on remembering the previous request's application state.

Example:

```
GET /api/students
Authorization: Bearer YOUR_TOKEN
```

The client sends the required authentication information with the request.

### 3. Cacheable

Responses should indicate whether they can be cached.

Caching helps reduce repeated requests and improve performance.

Example:

```
Cache-Control: max-age=60
```

This tells a client or cache that the response can be reused for up to 60 seconds, subject to the caching rules.

### 4. Uniform Interface

APIs should use consistent ways to identify and manipulate resources.

Example:

```
GET    /students
POST   /students
GET    /students/1
DELETE /students/1
```

### 5. Layered System

A client does not need to know every internal component between itself and the server.

For example:

```
CLIENT
   |
   v
LOAD BALANCER
   |
   v
API SERVER
   |
   v
DATABASE
```

### 6. Code on Demand (Optional)

A server can optionally send executable code to a client.

This constraint is optional in REST.

## 11. 🗂️ Resource-Based URLs

A resource is an object or collection of data that an API manages.

Examples:

- Students
- Employees
- Products
- Orders
- Users

REST APIs commonly use nouns in URLs to identify resources.

### Good URL design

```
GET    /api/students
GET    /api/students/1
POST   /api/students
DELETE /api/students/1
```

### Avoid action-based URLs when a standard HTTP method is enough

Less suitable:

```
GET /api/getStudents
POST /api/createStudent
GET /api/deleteStudent/1
```

Better:

```
GET    /api/students
POST   /api/students
DELETE /api/students/1
```

### Nested resource example

Suppose one student can have multiple courses.

```
GET /api/students/1/courses
```

This identifies the courses belonging to student 1.

### Query parameters

Query parameters are useful for filtering, searching and pagination.

Examples:

```
GET /api/students?course=Node.js
```

```
GET /api/students?page=1&limit=10
```

## 12. 🏗️ Practical Example — Student REST API

Now let's build a simple REST API using Express and raw JavaScript data.

### Step 1: Project structure

```
student-rest-api/
│
├── server.js
│
└── package.json
```

### Step 2: Install Express

```
npm init -y
npm install express
```

### Step 3: Create `server.js`

```
// Import Express
const express = require("express");

// Create Express application
const app = express();

// Port number
const PORT = 3000;

// Parse JSON request body
app.use(express.json());

// ===================================
// RAW STUDENT DATA
// ===================================

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

// ===================================
// GET: All students
// ===================================

app.get("/api/students", (req, res) => {

    res.status(200).json({

        success: true,

        message: "Students fetched successfully",

        data: students

    });

});

// ===================================
// GET: Student by ID
// ===================================

app.get("/api/students/:id", (req, res) => {

    const id = Number(req.params.id);

    const student = students.find((item) => item.id === id);

    if (!student) {

        return res.status(404).json({

            success: false,

            message: "Student not found"

        });

    }

    res.status(200).json({

        success: true,

        message: "Student found",

        data: student

    });

});

// ===================================
// POST: Create student
// ===================================

app.post("/api/students", (req, res) => {

    const { name, course, age } = req.body;

    if (!name || !course || age === undefined) {

        return res.status(400).json({

            success: false,

            message: "Name, course and age are required"

        });

    }

    const newStudent = {

        id: students.length
            ? Math.max(...students.map((item) => item.id)) + 1
            : 1,

        name,
        course,
        age

    };

    students.push(newStudent);

    res.status(201).json({

        success: true,

        message: "Student created successfully",

        data: newStudent

    });

});

// ===================================
// PUT: Update complete student
// ===================================

app.put("/api/students/:id", (req, res) => {

    const id = Number(req.params.id);

    const index = students.findIndex((item) => item.id === id);

    if (index === -1) {

        return res.status(404).json({

            success: false,

            message: "Student not found"

        });

    }

    const { name, course, age } = req.body;

    if (!name || !course || age === undefined) {

        return res.status(400).json({

            success: false,

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

        success: true,

        message: "Student updated successfully",

        data: students[index]

    });

});

// ===================================
// PATCH: Update selected fields
// ===================================

app.patch("/api/students/:id", (req, res) => {

    const id = Number(req.params.id);

    const student = students.find((item) => item.id === id);

    if (!student) {

        return res.status(404).json({

            success: false,

            message: "Student not found"

        });

    }

    const { name, course, age } = req.body;

    if (name !== undefined) student.name = name;

    if (course !== undefined) student.course = course;

    if (age !== undefined) student.age = age;

    res.status(200).json({

        success: true,

        message: "Student partially updated",

        data: student

    });

});

// ===================================
// DELETE: Delete student
// ===================================

app.delete("/api/students/:id", (req, res) => {

    const id = Number(req.params.id);

    const index = students.findIndex((item) => item.id === id);

    if (index === -1) {

        return res.status(404).json({

            success: false,

            message: "Student not found"

        });

    }

    const deletedStudent = students.splice(index, 1)[0];

    res.status(200).json({

        success: true,

        message: "Student deleted successfully",

        data: deletedStudent

    });

});

// ===================================
// START SERVER
// ===================================

app.listen(PORT, () => {

    console.log(`Server running on port ${PORT}`);

});
```

### Step 4: Run server

```
node server.js
```

Terminal:

```
Server running on port 3000
```

### Step 5: Test APIs using Postman

GET — Fetch all students

```
GET http://localhost:3000/api/students
```

GET — Fetch one student

```
GET http://localhost:3000/api/students/1
```

POST — Create student

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

PUT — Update complete student

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

PATCH — Update selected fields

```
PATCH http://localhost:3000/api/students/1
```

Body:

```
{
    "course": "Machine Learning"
}
```

DELETE — Delete student

```
DELETE http://localhost:3000/api/students/2
```

### Step 6: Understand raw data changes

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

After PATCH:

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

Important: The data is stored in memory only. It will reset when the server restarts. We will connect MongoDB in a later chapter.

## 13. ⚠️ Common Mistakes

### Mistake 1: Using GET to create data

Avoid:

```
GET /api/createStudent
```

Use:

```
POST /api/students
```

### Mistake 2: Using action names in URLs

Avoid:

```
GET /api/getStudents
```

Prefer:

```
GET /api/students
```

### Mistake 3: Forgetting JSON middleware

Incorrect:

```
app.post("/students", (req, res) => {

    console.log(req.body);

});
```

If JSON parsing middleware is missing, `req.body` may be undefined.

Correct:

```
app.use(express.json());
```

### Mistake 4: Returning incorrect status codes

For example, a successful creation should normally return:

```
res.status(201).json({
    message: "Created successfully"
});
```

### Mistake 5: Not validating request data

Always validate important fields before creating or updating resources.

## 14. ⭐ Best Practices

- Use nouns for resource URLs.
- Use the correct HTTP method.
- Return meaningful HTTP status codes.
- Use JSON consistently for API responses.
- Validate incoming data.
- Handle errors properly.
- Keep routes and controllers separate.
- Use authentication where required.
- Use pagination for large collections.
- Document API endpoints.

### Example of a clean API design

| Method | Endpoint            | Purpose           |
| ------ | ------------------- | ----------------- |
| GET    | `/api/students`     | Fetch students    |
| GET    | `/api/students/:id` | Fetch one student |
| POST   | `/api/students`     | Create student    |
| PUT    | `/api/students/:id` | Replace student   |
| PATCH  | `/api/students/:id` | Partially update  |
| DELETE | `/api/students/:id` | Delete student    |

## 15. 🎯 Interview Questions

## 16. 📝 Practice Problems

Try these exercises.

- Problem 1: Explain API, REST and REST API in your own words.
- Problem 2: Write five HTTP methods and their purposes.
- Problem 3: Design REST URLs for an Employee API.
- Problem 4: Design REST URLs for a Product API.
- Problem 5: Write a JSON object containing employee information.
- Problem 6: Create a REST API using Express.
- Problem 7: Test GET, POST, PUT, PATCH and DELETE using Postman.
- Problem 8: Explain stateless communication with an example.

## 17. 🏆 Mini Challenge — Product REST API

### Requirement

Create a Product REST API using Express.

### Initial raw data

```
let products = [
    {
        id: 1,
        name: "Laptop",
        price: 55000,
        category: "Electronics"
    },
    {
        id: 2,
        name: "Mobile",
        price: 25000,
        category: "Electronics"
    },
    {
        id: 3,
        name: "Keyboard",
        price: 1500,
        category: "Accessories"
    }
];
```

### Your tasks

1. Create a GET API to fetch all products.
2. Create a GET API to fetch a product by ID.
3. Create a POST API to add a product.
4. Create a PUT API to replace product details.
5. Create a PATCH API to update selected fields.
6. Create a DELETE API to remove a product.
7. Use proper HTTP status codes.
8. Return JSON responses.

### Expected endpoints

```
GET     /api/products
GET     /api/products/1
POST    /api/products
PUT     /api/products/1
PATCH   /api/products/1
DELETE  /api/products/1
```

### Logic-building steps

Step 1 — Requirement: Build a Product REST API.

Step 2 — Input: Product ID and product details.

Step 3 — Output: Product information in JSON.

Step 4 — Break into steps:

```
Create Express Server
        |
        v
Create Product Data
        |
        v
Create GET Routes
        |
        v
Create POST Route
        |
        v
Create PUT and PATCH Routes
        |
        v
Create DELETE Route
        |
        v
Test Using Postman
```

Step 5 — Hint:

```
app.use(express.json());
```

Step 6 — Pseudocode:

```
START

Create product array

GET all products
GET product by ID

POST new product
PUT complete product
PATCH selected fields

DELETE product

Return JSON responses

END
```

Step 7 — Your turn!

Try to write the code yourself. Send your attempt, and I will review it line by line. I will not reveal the complete mini-challenge solution unless you ask.

## 18. 📌 Chapter Summary & Quick Revision

### What did we learn?

| Concept   | Meaning                                   |
| --------- | ----------------------------------------- |
| API       | Communication interface                   |
| REST      | Architectural style                       |
| REST API  | API designed using REST                   |
| Client    | Sends requests                            |
| Server    | Processes requests                        |
| HTTP      | Communication protocol                    |
| JSON      | Data exchange format                      |
| GET       | Read data                                 |
| POST      | Create data                               |
| PUT       | Replace data                              |
| PATCH     | Partially update data                     |
| DELETE    | Remove data                               |
| Stateless | Each request carries required information |
| Resource  | Data managed by an API                    |

### Final revision flow

```
REACT FRONTEND
      |
      | HTTP Request
      v
EXPRESS REST API
      |
      | Process Request
      v
CONTROLLER
      |
      v
DATABASE
      |
      v
JSON RESPONSE
      |
      v
REACT FRONTEND
```

### Self-check

- I understand what an API is.
- I understand REST and REST API.
- I understand client-server architecture.
- I know the five common HTTP methods.
- I understand HTTP requests and responses.
- I can write JSON data.
- I understand REST principles.
- I can design resource-based URLs.
- I can create a basic REST API using Express.

## 🎓 Next Chapter

Chapter 24 — REST API Request Parameters

We will learn:

- What are request parameters?
- Route parameters (`req.params`)
- Query parameters (`req.query`)
- Request body (`req.body`)
- Request headers (`req.headers`)
- Difference between params, query and body
- Practical filtering and searching
- Pagination using query parameters
- Postman testing
- Real-world Student API examples

Type `NEXT` to start Chapter 24.