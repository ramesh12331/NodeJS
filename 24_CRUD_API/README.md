# 🚀 PART 6 — REST API DEVELOPMENT

# Chapter 24 — REST API Request Parameters

BEGINNER LEVEL → PRACTICAL LEVEL

## 📚 Table of Contents

1. What are Request Parameters?
2. Why do we need Request Parameters?
3. Real-world Analogy
4. Types of Request Data
5. Route Parameters — `req.params`
6. Query Parameters — `req.query`
7. Request Body — `req.body`
8. Request Headers — `req.headers`
9. Difference Between Params, Query and Body
10. Practical Example — Student API
11. Filtering, Searching and Pagination
12. Common Mistakes
13. Best Practices
14. Interview Questions
15. Practice Problems
16. Mini Challenge
17. Chapter Summary & Quick Revision

## 1. 🧠 What are Request Parameters?

When a client sends a request to an Express server, it can send additional information.

This information is called request data.

For example, imagine you want to get student ID 10.

```
GET /api/students/10
```

Here, `10` is the student ID.

Or you want to filter students by course:

```
GET /api/students?course=Node.js
```

Here, `course=Node.js` is a query parameter.

Or you want to create a student:

```
{
    "name": "Ramesh",
    "course": "Node.js",
    "age": 25
}
```

This information is sent in the request body.

Express provides different properties to access this information:

| Property      | Purpose               |
| ------------- | --------------------- |
| `req.params`  | Read route parameters |
| `req.query`   | Read query parameters |
| `req.body`    | Read request body     |
| `req.headers` | Read request headers  |

## 2. 🤔 Why do we need Request Parameters?

Imagine your Student API contains 100 students.

You may want to:

- Get student ID 10.
- Get only Node.js students.
- Search for students named Ramesh.
- Create a new student.
- Update student information.
- Send an authentication token.

We use request parameters and other request data to perform these operations.

## 3. 🌍 Real-world Analogy

Imagine ordering food online.

You provide:

- Product ID
- Food category
- Quantity
- Delivery address
- Authentication information

Each piece of information helps the application understand your request.

Express receives request information in a similar way.

## 4. 🔄 Types of Request Data

Let's understand the four important types.

```
CLIENT REQUEST
      |
      v
EXPRESS SERVER
      |
      +---- req.params
      |       Route values
      |
      +---- req.query
      |       Filtering values
      |
      +---- req.body
      |       Submitted data
      |
      +---- req.headers
              Metadata and tokens
```

Example request:

```
POST /api/students/10?active=true
Content-Type: application/json
Authorization: Bearer example-token
```

Body:

```
{
    "name": "Ramesh",
    "course": "Node.js",
    "age": 25
}
```

Here:

- `10` → `req.params.id`
- `active=true` → `req.query.active`
- Student details → `req.body`
- Authorization token → `req.headers.authorization`

## 5. 🔢 Route Parameters — `req.params`

Route parameters are values captured from named placeholders in the URL path.

They are commonly used to identify a specific resource.

### Example

```
GET /api/students/10
```

Route:

```
app.get("/api/students/:id", (req, res) => {

    console.log(req.params);

    res.json({
        id: req.params.id
    });

});
```

### Output

```
{
    "id": "10"
}
```

Notice that the value is a string.

### Understanding `:id`

```
"/api/students/:id"
```

Here:

- `:` means a route parameter.
- `id` is the parameter name.

You can use any meaningful name.

```
app.get("/api/employees/:employeeId", (req, res) => {

    console.log(req.params.employeeId);

});
```

Request:

```
GET /api/employees/25
```

Output:

```
25
```

### Multiple route parameters

You can use multiple parameters in one route.

```
app.get("/api/students/:studentId/courses/:courseId", (req, res) => {

    const studentId = req.params.studentId;

    const courseId = req.params.courseId;

    res.json({
        studentId,
        courseId
    });

});
```

Request:

```
GET /api/students/10/courses/5
```

Response:

```
{
    "studentId": "10",
    "courseId": "5"
}
```

### Important: Convert numeric values

Route parameters are strings by default.

```
const id = Number(req.params.id);
```

Now `id` is a number.

## 6. 🔍 Query Parameters — `req.query`

Query parameters are values sent after `?` in the URL.

They are commonly used for:

- Filtering
- Searching
- Sorting
- Pagination

### Example

```
GET /api/students?course=Node.js
```

Route:

```
app.get("/api/students", (req, res) => {

    console.log(req.query);

    res.json({
        course: req.query.course
    });

});
```

### Output

```
{
    "course": "Node.js"
}
```

### Multiple query parameters

Request:

```
GET /api/students?course=Node.js&age=25
```

Code:

```
app.get("/api/students", (req, res) => {

    const course = req.query.course;

    const age = req.query.age;

    res.json({
        course,
        age
    });

});
```

Response:

```
{
    "course": "Node.js",
    "age": "25"
}
```

### Query parameters are optional

You can request:

```
GET /api/students
```

Or:

```
GET /api/students?course=Python
```

The same route can handle both requests.

### Query parameters with multiple values

Example:

```
GET /api/students?course=Node.js&course=Python
```

Depending on the query parser configuration, Express can represent repeated query keys as an array.

For normal beginner examples, use one value per query key.

## 7. 📦 Request Body — `req.body`

The request body contains data sent by the client to the server.

It is commonly used with:

- POST
- PUT
- PATCH

### Example request

```
POST /api/students
Content-Type: application/json
```

Body:

```
{
    "name": "Anil",
    "course": "FastAPI",
    "age": 23
}
```

### Express code

```
const express = require("express");

const app = express();

// Middleware to parse JSON
app.use(express.json());

app.post("/api/students", (req, res) => {

    console.log(req.body);

    res.json({
        message: "Student data received",
        data: req.body
    });

});
```

### Output

```
{
    "message": "Student data received",
    "data": {
        "name": "Anil",
        "course": "FastAPI",
        "age": 23
    }
}
```

### Important

Without this middleware:

```
app.use(express.json());
```

Express will not automatically parse incoming JSON request bodies.

For HTML form submissions encoded as URL-encoded data, use:

```
app.use(express.urlencoded({ extended: true }));
```

## 8. 🔐 Request Headers — `req.headers`

Request headers contain additional information about an HTTP request.

Headers can provide:

- Content type
- Authentication token
- Accepted response formats
- Client information

### Example request

```
GET /api/students
Authorization: Bearer example-token
Content-Type: application/json
```

### Express code

```
app.get("/api/students", (req, res) => {

    const authorization = req.headers.authorization;

    res.json({
        authorization
    });

});
```

Response:

```
{
    "authorization": "Bearer example-token"
}
```

### Common headers

| Header          | Purpose                               |
| --------------- | ------------------------------------- |
| `Content-Type`  | Describes request body format         |
| `Authorization` | Carries authentication credentials    |
| `Accept`        | Indicates acceptable response formats |
| `User-Agent`    | Identifies the client software        |

Important: Never send real passwords or secret API keys in URLs. Use secure authentication mechanisms and HTTPS.

## 9. 📊 Difference Between Params, Query and Body

This is an important interview topic.

| Feature    | `req.params`      | `req.query`       | `req.body`             |
| ---------- | ----------------- | ----------------- | ---------------------- |
| Location   | URL path          | After `?`         | Request body           |
| Purpose    | Identify resource | Filter/search     | Send data              |
| Example    | `/students/10`    | `?course=Node.js` | Student JSON           |
| Common use | Get by ID         | Search students   | Create student         |
| Value type | Usually strings   | Usually strings   | Depends on parsed JSON |

### One example containing all three

Request:

```
PATCH /api/students/10?notify=true
Content-Type: application/json
Authorization: Bearer example-token
```

Body:

```
{
    "course": "Machine Learning"
}
```

Code:

```
app.patch("/api/students/:id", (req, res) => {

    const id = req.params.id;

    const notify = req.query.notify;

    const course = req.body.course;

    const authorization = req.headers.authorization;

    res.json({
        id,
        notify,
        course,
        authorization
    });

});
```

Response:

```
{
    "id": "10",
    "notify": "true",
    "course": "Machine Learning",
    "authorization": "Bearer example-token"
}
```

### Easy memory trick

- `params` → Which resource?
- `query` → Which filter?
- `body` → What data?
- `headers` → What additional request information?

## 10. 🏗️ Practical Example — Student API

Let's create an API using all four request properties.

### Step 1: Project structure

```
student-api/
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

// Create application
const app = express();

// Port number
const PORT = 3000;

// Parse JSON request body
app.use(express.json());

// ===================================
// RAW STUDENT DATA
// ===================================

let students = [
    { id: 1, name: "Ramesh", course: "Node.js", age: 25 },
    { id: 2, name: "Kumar", course: "React.js", age: 24 },
    { id: 3, name: "Suresh", course: "Python", age: 26 },
    { id: 4, name: "Anil", course: "Node.js", age: 23 },
    { id: 5, name: "Raj", course: "Python", age: 25 }
];

// ===================================
// GET: All students
// ===================================

app.get("/api/students", (req, res) => {

    res.status(200).json({
        message: "Students fetched successfully",
        data: students
    });

});

// ===================================
// GET: Student by ID
// Uses req.params
// ===================================

app.get("/api/students/:id", (req, res) => {

    // Read ID from URL
    const id = Number(req.params.id);

    // Find student
    const student = students.find((item) => item.id === id);

    if (!student) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    res.status(200).json({
        message: "Student found",
        data: student
    });

});

// ===================================
// GET: Filter students by course
// Uses req.query
// ===================================

app.get("/api/filter-students", (req, res) => {

    // Read course from query
    const course = req.query.course;

    // Filter students
    const filteredStudents = students.filter(
        (item) => item.course.toLowerCase() === String(course || "").toLowerCase()
    );

    res.status(200).json({
        message: "Filtered students",
        data: filteredStudents
    });

});

// ===================================
// POST: Create student
// Uses req.body
// ===================================

app.post("/api/students", (req, res) => {

    // Read body data
    const { name, course, age } = req.body;

    // Validate fields
    if (!name || !course || age === undefined) {

        return res.status(400).json({
            message: "Name, course and age are required"
        });

    }

    // Create student
    const newStudent = {
        id: students.length
            ? Math.max(...students.map((item) => item.id)) + 1
            : 1,
        name,
        course,
        age
    };

    // Add student
    students.push(newStudent);

    res.status(201).json({
        message: "Student created successfully",
        data: newStudent
    });

});

// ===================================
// GET: Read authorization header
// Uses req.headers
// ===================================

app.get("/api/check-header", (req, res) => {

    const authorization = req.headers.authorization;

    res.status(200).json({
        message: "Header received",
        authorization: authorization || "No authorization header"
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

### Step 5: Test using Postman

Test 1 — Get all students

```
GET http://localhost:3000/api/students
```

Test 2 — Get student by ID

```
GET http://localhost:3000/api/students/2
```

Expected response:

```
{
    "message": "Student found",
    "data": {
        "id": 2,
        "name": "Kumar",
        "course": "React.js",
        "age": 24
    }
}
```

Test 3 — Filter students

```
GET http://localhost:3000/api/filter-students?course=Node.js
```

Expected response:

```
{
    "message": "Filtered students",
    "data": [
        {
            "id": 1,
            "name": "Ramesh",
            "course": "Node.js",
            "age": 25
        },
        {
            "id": 4,
            "name": "Anil",
            "course": "Node.js",
            "age": 23
        }
    ]
}
```

Test 4 — Create student

```
POST http://localhost:3000/api/students
```

Body → raw → JSON:

```
{
    "name": "Venkat",
    "course": "FastAPI",
    "age": 24
}
```

Test 5 — Send request header

```
GET http://localhost:3000/api/check-header
```

In Postman:

1. Open the Headers tab.
2. Enter key: `Authorization`.
3. Enter value: `Bearer example-token`.
4. Send the request.

Expected response:

```
{
    "message": "Header received",
    "authorization": "Bearer example-token"
}
```

## 11. 🔎 Filtering, Searching and Pagination

Query parameters are especially useful when working with large datasets.

### A. Filtering

Filtering means retrieving records that match a condition.

Request:

```
GET /api/students?course=Node.js
```

Code:

```
const filteredStudents = students.filter(
    (item) => item.course === req.query.course
);
```

Raw data:

```
[
    { id: 1, name: "Ramesh", course: "Node.js", age: 25 },
    { id: 2, name: "Kumar", course: "React.js", age: 24 },
    { id: 3, name: "Suresh", course: "Python", age: 26 }
]
```

After filtering:

```
[
    { id: 1, name: "Ramesh", course: "Node.js", age: 25 }
]
```

### B. Searching

Searching means finding records based on matching text.

Request:

```
GET /api/students/search?name=ram
```

Code:

```
app.get("/api/students/search", (req, res) => {

    const name = String(req.query.name || "").toLowerCase();

    const result = students.filter((item) =>
        item.name.toLowerCase().includes(name)
    );

    res.json({
        data: result
    });

});
```

Here, `.includes()` checks whether the name contains the search text.

For example:

```
"Ramesh".toLowerCase().includes("ram");
```

Output:

```
true
```

### C. Pagination

Pagination means dividing a large collection into smaller pages.

Imagine you have 100 students.

Instead of returning all 100 records, you can return 10 records per page.

Request:

```
GET /api/students?page=1&limit=2
```

Code:

```
app.get("/api/students/paginated", (req, res) => {

    // Read query parameters
    const page = Math.max(1, Number(req.query.page) || 1);

    const limit = Math.max(1, Number(req.query.limit) || 2);

    // Calculate starting position
    const startIndex = (page - 1) * limit;

    // Get required records
    const result = students.slice(startIndex, startIndex + limit);

    res.json({
        page,
        limit,
        totalStudents: students.length,
        totalPages: Math.ceil(students.length / limit),
        data: result
    });

});
```

Request:

```
GET /api/students/paginated?page=1&limit=2
```

Expected response:

```
{
    "page": 1,
    "limit": 2,
    "totalStudents": 5,
    "totalPages": 3,
    "data": [
        {
            "id": 1,
            "name": "Ramesh",
            "course": "Node.js",
            "age": 25
        },
        {
            "id": 2,
            "name": "Kumar",
            "course": "React.js",
            "age": 24
        }
    ]
}
```

### Pagination dry run

Formula:

```
startIndex = (page - 1) * limit;
```

For page 1 and limit 2:

```
startIndex = (1 - 1) * 2
           = 0
```

For page 2 and limit 2:

```
startIndex = (2 - 1) * 2
           = 2
```

For page 3 and limit 2:

```
startIndex = (3 - 1) * 2
           = 4
```

| Page | Start index | Returned records |
| ---- | ----------- | ---------------- |
| 1    | 0           | 1, 2             |
| 2    | 2           | 3, 4             |
| 3    | 4           | 5                |

Note: In real applications, validate maximum page limits and perform pagination in the database rather than loading every record into memory.

## 12. ⚠️ Common Mistakes

### Mistake 1: Forgetting `express.json()`

Incorrect:

```
app.post("/students", (req, res) => {

    console.log(req.body);

});
```

Correct:

```
app.use(express.json());
```

### Mistake 2: Forgetting to convert route IDs

Incorrect:

```
const id = req.params.id;

const student = students.find((item) => item.id === id);
```

The URL value is a string, while the data ID is a number.

Correct:

```
const id = Number(req.params.id);
```

### Mistake 3: Reading query data from params

Incorrect:

```
const course = req.params.course;
```

For:

```
/api/students?course=Node.js
```

Correct:

```
const course = req.query.course;
```

### Mistake 4: Reading body data from query

Incorrect:

```
const name = req.query.name;
```

For a POST request with JSON body:

```
{
    "name": "Ramesh"
}
```

Correct:

```
const name = req.body.name;
```

### Mistake 5: Not validating query values

Incorrect:

```
const limit = Number(req.query.limit);
```

If the user sends an invalid value, `limit` may become `NaN`.

Better:

```
const limit = Math.max(1, Number(req.query.limit) || 10);
```

## 13. ⭐ Best Practices

1. Use `req.params` for identifying resources.
2. Use `req.query` for filters, search and pagination.
3. Use `req.body` for submitted data.
4. Use `req.headers` for request metadata and authentication information.
5. Convert values to the expected type.
6. Validate all user input.
7. Set sensible pagination limits.
8. Do not send sensitive information in URL parameters.
9. Use HTTPS when transmitting sensitive information.
10. Return meaningful JSON responses and status codes.

## 14. 🎯 Interview Questions

## 15. 📝 Practice Problems

Try these exercises yourself.

- Problem 1: Create an API using `req.params` to fetch an employee by ID.
- Problem 2: Create an API using `req.query` to filter products by category.
- Problem 3: Create a POST API using `req.body`.
- Problem 4: Read the Authorization header using `req.headers`.
- Problem 5: Create a search API using a name query.
- Problem 6: Create pagination using `page` and `limit`.
- Problem 7: Create an API that uses params, query, body and headers together.

## 16. 🏆 Mini Challenge — Employee Search API

### Requirement

Create an Employee API with route parameters, query parameters and request body.

### Initial raw data

```
let employees = [
    { id: 1, name: "Ramesh", department: "IT", salary: 30000 },
    { id: 2, name: "Kumar", department: "HR", salary: 25000 },
    { id: 3, name: "Suresh", department: "Finance", salary: 35000 },
    { id: 4, name: "Anil", department: "IT", salary: 40000 },
    { id: 5, name: "Raj", department: "HR", salary: 28000 }
];
```

### Your tasks

1. Create GET all employees.
2. Create GET employee by ID using `req.params`.
3. Create department filtering using `req.query`.
4. Create name searching using `req.query`.
5. Create POST employee using `req.body`.
6. Create pagination using `page` and `limit`.

### Expected URLs

```
GET /api/employees

GET /api/employees/1

GET /api/employees?department=IT

GET /api/employees/search?name=ram

GET /api/employees/paginated?page=1&limit=2

POST /api/employees
```

### Logic-building steps

Step 1 — Requirement: Build an Employee API with different request data types.

Step 2 — Input: Employee ID, department, search name and employee details.

Step 3 — Output: Employee records in JSON.

Step 4 — Break into steps:

```
Create Express Server
        |
        v
Create Employee Array
        |
        v
GET All Employees
        |
        v
GET Employee By ID
        |
        v
Filter by Department
        |
        v
Search by Name
        |
        v
POST Employee
        |
        v
Pagination
```

Step 5 — Hints

```
req.params.id

req.query.department

req.query.name

req.body
```

Step 6 — Pseudocode

```
START

Create employee array

Read employee ID from params

Read department from query

Read search name from query

Read employee details from body

Calculate pagination

Send JSON responses

END
```

Step 7 — Your turn!

Try the challenge yourself. Send your code, and I will review it line by line. I will not provide the complete solution unless you ask.

## 17. 📌 Chapter Summary & Quick Revision

### What did we learn?

| Concept       | Meaning                   | Example            |
| ------------- | ------------------------- | ------------------ |
| `req.params`  | Route values              | `/students/10`     |
| `req.query`   | Query values              | `?course=Node.js`  |
| `req.body`    | Submitted data            | JSON body          |
| `req.headers` | Request metadata          | Authorization      |
| Filtering     | Select matching records   | `?course=Python`   |
| Searching     | Find matching text        | `?name=ram`        |
| Pagination    | Divide records into pages | `?page=1&limit=10` |

### Quick memory trick

```
PARAMS  = WHICH RESOURCE?
QUERY   = WHICH FILTER?
BODY    = WHAT DATA?
HEADERS = WHAT REQUEST INFORMATION?
```

### Self-check

- I understand `req.params`.
- I understand `req.query`.
- I understand `req.body`.
- I understand `req.headers`.
- I can filter data.
- I can search data.
- I can implement pagination.
- I can test requests using Postman.

## 🎓 Next Chapter

Chapter 25 — REST API Validation

We will learn:

- What is API validation?
- Why is validation important?
- Required field validation
- String validation
- Number validation
- Email validation
- Custom validation middleware
- Express-validator introduction
- Practical Student API validation
- Handling validation errors

Type `NEXT` to start Chapter 25.