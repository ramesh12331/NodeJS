# Chapter 23 — REST API Fundamentals



PART 6 — REST API DEVELOPMENT

Beginner to Advanced



## 🔑 Requires Before Starting

Before learning REST APIs, you should understand:

1. Node.js: JavaScript runtime used for backend development.
2. Express.js: Framework used to create backend APIs.
3. Routing: Handling requests using GET, POST, PUT, PATCH and DELETE.
4. Express Router: Organizing API routes into separate files.
5. Controllers: Functions that handle requests and responses.
6. Middleware: Functions that execute during the request-response lifecycle.
7. Error handling: Managing errors using `try/catch` and error middleware.
8. HTTP: Understanding how clients and servers communicate.
9. JSON: A format used to exchange data between frontend and backend.

You have already learned most of these concepts. Now we will understand how to combine them to build professional REST APIs.

## 1. What is REST?

REST stands for Representational State Transfer.

REST is an architectural style used to design web APIs.

It provides guidelines for how clients and servers communicate using HTTP.

For example, imagine you are building a Student Management application.

Your React frontend needs to communicate with your Express backend.

The frontend may need to:

- Get all students.
- Get one student.
- Create a student.
- Update a student.
- Delete a student.

REST helps us organize these operations using resources and HTTP methods.

### Simple example

```
GET     /api/students
POST    /api/students
GET     /api/students/101
PUT     /api/students/101
DELETE  /api/students/101
```

These are REST-style API endpoints.

### 📖 Read

📖 Read — Understand REST

### 💡 Important

💡 Important — Remember

## 2. Why do we need REST APIs?

Imagine you have developed:

- React frontend.
- Node.js backend.
- PostgreSQL database.

Your frontend needs student information from your backend.

Without a common API structure, different developers might create inconsistent URLs and methods.

For example:

```
/getAllStudents
/createNewStudent
/updateStudentDetails
/removeStudent
```

These endpoints can work, but they do not follow common REST naming conventions.

REST provides a consistent approach:

```
GET     /students
POST    /students
PUT     /students/101
DELETE  /students/101
```

### Benefits of REST APIs

1. Standard communication between frontend and backend.
2. Clear resource-based URLs.
3. Uses standard HTTP methods.
4. Supports different frontend technologies.
5. Easier to maintain.
6. Easier to integrate with mobile applications.
7. Supports scalable application architecture.

### Real application example

[APIs Without Tears: A Gentle Intro to FastAPI | by chaithanya k | Medium](https://images.openai.com/static-rsc-4/1OhcETPaVubr_bAqX2pd5-pGEZmZsiXKYdZRnZSyUP60y5Cd33DlfKz1ZW9fDHz5tfvGxqMgT4oEyGJLxkv7aMl_z2j4WuwwtN8lqVx79L-hwkuBKlaDYA0XtFVwy9q0kLIw6N43nIqf5HlWsFjbNO6qMTCe-gci0xT5s9jlPFY?purpose=inline)

[medium.com](https://medium.com/%40cchaithanya83/apis-without-tears-a-gentle-intro-to-fastapi-ba3667a10bd3?utm_source=chatgpt.com)

```
React Frontend
      |
      | HTTP Request
      ↓
Express REST API
      |
      | Database Query
      ↓
PostgreSQL / MongoDB
```

The frontend does not need to know how the database stores the information. It communicates with the backend through API endpoints.

## 3. Real-world analogy

Imagine a restaurant.

[Food & Beverage POS & Payment Solutions | Elavon UK](https://images.openai.com/static-rsc-4/-ymKE8OGV_3LVrBOlG9XJisvrZq8WN8f82czZHmslCHR4VGEUMktv8I2hiNKfUa1_mGdXDCFJAWI1c9ryv9_Sw_D54D_eccils8UcRNMppDiJVBohii5qhDUB-X9n8z6RSLupPUDJaXCOiR03YUhdDg5K8omUUoSJoJpndyp4dU?purpose=inline)

[elavon.co.uk](https://www.elavon.co.uk/about/industries-we-work-with/food-and-beverage.html?utm_source=chatgpt.com)

The process:

1. Customer requests food.
2. Waiter receives the request.
3. Kitchen prepares the food.
4. Waiter delivers the food.

REST API works similarly.

| Restaurant     | REST API          |
| -------------- | ----------------- |
| Customer       | Frontend client   |
| Menu           | API documentation |
| Food request   | HTTP request      |
| Waiter         | API endpoint      |
| Kitchen        | Backend logic     |
| Food delivered | API response      |

The frontend sends a request, the backend processes it, and the backend sends a response.

## 4. Architecture / Flow

### REST API architecture

Frontend

React / Mobile App / Browser

HTTP Request

REST API

Express.js

Database operations

Database

MongoDB / PostgreSQL

Query result

Express API Response

JSON + HTTP status code

HTTP Response

Frontend Displays Data

### GitHub Mermaid diagram

Copy this diagram directly into your GitHub README.

\#chatgpt-mermaid-\_r_6ts\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_6ts\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_6ts\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_6ts\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_6ts\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6ts\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_6ts\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_6ts\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_6ts\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_6ts\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_6ts\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_6ts\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_6ts\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_6ts\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_6ts\_ p{margin:0;}#chatgpt-mermaid-\_r_6ts\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6ts\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6ts\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6ts\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_6ts\_ .label text,#chatgpt-mermaid-\_r_6ts\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6ts\_ .node rect,#chatgpt-mermaid-\_r_6ts\_ .node circle,#chatgpt-mermaid-\_r_6ts\_ .node ellipse,#chatgpt-mermaid-\_r_6ts\_ .node polygon,#chatgpt-mermaid-\_r_6ts\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_6ts\_ .rough-node .label text,#chatgpt-mermaid-\_r_6ts\_ .node .label text,#chatgpt-mermaid-\_r_6ts\_ .image-shape .label,#chatgpt-mermaid-\_r_6ts\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_6ts\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_6ts\_ .rough-node .label,#chatgpt-mermaid-\_r_6ts\_ .node .label,#chatgpt-mermaid-\_r_6ts\_ .image-shape .label,#chatgpt-mermaid-\_r_6ts\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_6ts\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_6ts\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_6ts\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_6ts\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_6ts\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_6ts\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_6ts\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_6ts\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_6ts\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_6ts\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_6ts\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6ts\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6ts\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_6ts\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_6ts\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_6ts\_ .icon-shape,#chatgpt-mermaid-\_r_6ts\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_6ts\_ .icon-shape p,#chatgpt-mermaid-\_r_6ts\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_6ts\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_6ts\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_6ts\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_6ts\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_6ts\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_6ts\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_6ts\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_6ts\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_6ts\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_6ts\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_6ts\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_6ts\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_6ts\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_6ts\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_6ts\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_6ts\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_6ts\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_6ts\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_6ts\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_6ts\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_6ts\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_6ts\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_6ts\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_6ts\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_6ts\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_6ts\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_6ts\_ .node rect,#chatgpt-mermaid-\_r_6ts\_ .node circle,#chatgpt-mermaid-\_r_6ts\_ .node ellipse,#chatgpt-mermaid-\_r_6ts\_ .node polygon,#chatgpt-mermaid-\_r_6ts\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_6ts\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_6ts\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_6ts\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_6ts\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_6ts\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}React FrontendExpress REST APIRouterControllerDatabaseJSON ResponseHTTP Request

### Request-response example

Frontend sends:

```
GET /api/students
```

Backend responds:

```
{
    "success": true,
    "data": [
        {
            "id": 1,
            "name": "Ramesh"
        },
        {
            "id": 2,
            "name": "Suresh"
        }
    ]
}
```

## 5. Syntax

Now let's understand the important REST API concepts.

### 5.1 REST

REST is an architectural style for designing APIs.

### 5.2 Resource

A resource is an entity or data object that an API manages.

Examples:

```
Students
Employees
Products
Customers
Orders
Books
```

### 5.3 Endpoint

An endpoint is a URL through which a client accesses a resource or performs an operation.

Example:

```
/api/students
```

### 5.4 HTTP methods

| Method | Purpose                     |
| ------ | --------------------------- |
| GET    | Read data                   |
| POST   | Create data                 |
| PUT    | Replace/update a resource   |
| PATCH  | Partially update a resource |
| DELETE | Delete data                 |

### 5.5 JSON

JSON stands for JavaScript Object Notation.

Example:

```
{
    "id": 101,
    "name": "Ramesh",
    "email": "ramesh@example.com"
}
```

### 5.6 HTTP request structure

A request commonly contains:

```
HTTP Method
URL
Headers
Body (when applicable)
```

Example:

```
POST /api/students
Content-Type: application/json
```

Body:

```
{
    "name": "Ramesh",
    "email": "ramesh@example.com"
}
```

## 6. Basic example

Let's create a simple REST API using Express.

### Step 1: Create project

```
mkdir 23_REST_API_Fundamentals

cd 23_REST_API_Fundamentals

npm init -y

npm install express
```

### Step 2: Project structure

```
23_REST_API_Fundamentals/
│
├── node_modules/
├── server.js
└── package.json
```

### Step 3: Create `server.js`

```
const express = require("express");

const app = express();

// Middleware to read JSON
app.use(express.json());

// Sample student data
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

// GET - Read students
app.get("/api/students", (req, res) => {

    res.status(200).json({

        message: "Students fetched successfully",

        data: students

    });

});

// GET - Read single student
app.get("/api/students/:id", (req, res) => {

    const id = Number(req.params.id);

    const student = students.find(
        (student) => student.id === id
    );

    if (!student) {

        return res.status(404).json({

            message: "Student not found"

        });

    }

    res.status(200).json({

        data: student

    });

});

// Start server
app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

### Step 4: Start server

```
node server.js
```

Test in Postman:

```
GET http://localhost:3000/api/students
```

## 7. Dry run

Let's understand this request:

```
GET /api/students/1
```

### Step-by-step execution

Step 1: Client sends a GET request.

```
/api/students/1
```

Step 2: Express matches this route.

```
app.get("/api/students/:id", (req, res) => {
```

Step 3: Express reads the ID.

```
const id = Number(req.params.id);
```

Value:

```
id = 1
```

Step 4: Find the student.

```
const student = students.find(
    (student) => student.id === id
);
```

The array contains a student with ID 1.

Step 5: Send the response.

```
res.status(200).json({
    data: student
});
```

### Execution flow

```
Client
  ↓
GET /api/students/1
  ↓
Express Route
  ↓
Read ID
  ↓
Find Student
  ↓
Send JSON Response
```

## 8. Output

### GET all students

Request:

```
GET http://localhost:3000/api/students
```

Response:

```
{
    "message": "Students fetched successfully",
    "data": [
        {
            "id": 1,
            "name": "Ramesh"
        },
        {
            "id": 2,
            "name": "Suresh"
        }
    ]
}
```

### GET single student

Request:

```
GET http://localhost:3000/api/students/1
```

Response:

```
{
    "data": {
        "id": 1,
        "name": "Ramesh"
    }
}
```

### Student not found

Request:

```
GET http://localhost:3000/api/students/99
```

Response:

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

Let's understand the most important lines.

### Express setup

```
const express = require("express");
```

Imports the Express framework.

```
const app = express();
```

Creates the Express application.

```
app.use(express.json());
```

Parses incoming JSON request bodies.

### Resource definition

```
const students = [
    { id: 1, name: "Ramesh" },
    { id: 2, name: "Suresh" }
];
```

Creates sample student records.

### GET endpoint

```
app.get("/api/students", (req, res) => {
```

Creates a GET endpoint for the students resource.

```
res.status(200).json({
    data: students
});
```

Sends student data with HTTP status `200 OK`.

### Route parameter

```
req.params.id
```

Reads the ID from the URL.

Example:

```
/api/students/101
```

Here:

```
req.params.id = "101"
```

The value is initially a string, which is why we convert it using `Number()` when we need a numeric ID.

## 10. Practical example

Now let's understand all the important REST API concepts in detail.

### 10.1 Resources

A resource represents the data managed by an API.

For example, an online shopping application may have:

```
Users
Products
Orders
Categories
Payments
Reviews
```

Common REST resource names are usually plural nouns.

Examples:

```
/api/users
/api/products
/api/orders
```

### 10.2 Endpoints

An endpoint is an API URL used to access or operate on a resource.

For example:

```
/api/products
/api/products/101
/api/orders
/api/users/5
```

Understand:

| Endpoint            | Meaning             |
| ------------------- | ------------------- |
| `/api/products`     | Product collection  |
| `/api/products/101` | Product with ID 101 |
| `/api/orders`       | Order collection    |
| `/api/users/5`      | User with ID 5      |

### 10.3 HTTP methods

Let's understand each method.

A. GET — Read data

GET retrieves information.

```
app.get("/api/students", (req, res) => {

    res.json({
        message: "Get all students"
    });

});
```

Example:

```
GET /api/students
```

B. POST — Create data

POST creates a new resource.

```
app.post("/api/students", (req, res) => {

    const student = req.body;

    res.status(201).json({
        message: "Student created",
        data: student
    });

});
```

Example body:

```
{
    "name": "Ramesh",
    "email": "ramesh@example.com"
}
```

C. PUT — Replace a resource

PUT generally replaces the resource representation with the supplied data.

```
app.put("/api/students/:id", (req, res) => {

    const id = req.params.id;

    const student = req.body;

    res.json({
        message: "Student replaced",
        id,
        data: student
    });

});
```

D. PATCH — Partially update a resource

PATCH updates selected fields.

```
app.patch("/api/students/:id", (req, res) => {

    const id = req.params.id;

    const updates = req.body;

    res.json({
        message: "Student partially updated",
        id,
        updates
    });

});
```

E. DELETE — Delete a resource

DELETE removes a resource.

```
app.delete("/api/students/:id", (req, res) => {

    const id = req.params.id;

    res.json({
        message: "Student deleted",
        id
    });

});
```

### 10.4 CRUD

CRUD stands for:

- Create
- Read
- Update
- Delete

| CRUD operation | HTTP method | Endpoint            |
| -------------- | ----------- | ------------------- |
| Create         | POST        | `/api/students`     |
| Read all       | GET         | `/api/students`     |
| Read one       | GET         | `/api/students/:id` |
| Update         | PUT         | `/api/students/:id` |
| Partial update | PATCH       | `/api/students/:id` |
| Delete         | DELETE      | `/api/students/:id` |

### 10.5 Stateless architecture

Statelessness is one of the important REST principles.

Stateless means the server does not store client session state between requests as part of the REST interaction.

Each request should contain the information needed to process it.

For example, an authenticated request may include an access token:

```
GET /api/profile
Authorization: Bearer your-access-token
```

The server verifies the token and processes the request.

It does not depend on remembering the previous request from that client.

💡 Important distinction

Stateless does not mean the server cannot store data. Your backend can still store users, products, orders, and other information in a database. It means each request is handled independently with the necessary request information.

### 10.6 JSON API

A JSON API commonly sends and receives JSON data.

Example request:

```
{
    "name": "Ramesh",
    "email": "ramesh@example.com"
}
```

Example response:

```
{
    "success": true,
    "message": "Student created successfully",
    "data": {
        "id": 101,
        "name": "Ramesh",
        "email": "ramesh@example.com"
    }
}
```

JSON is commonly used because it is easy to exchange between JavaScript frontend and backend applications.

### 10.7 REST conventions

Follow these common conventions when designing APIs.

Convention 1: Use nouns instead of verbs.

Avoid:

```
/getStudents
/createStudent
/deleteStudent
```

Prefer:

```
GET     /api/students
POST    /api/students
DELETE  /api/students/101
```

Convention 2: Use plural resource names.

Prefer:

```
/api/students
/api/products
/api/employees
```

Convention 3: Use route parameters for individual resources.

```
/api/students/101
/api/products/501
```

Convention 4: Use query parameters for filtering and pagination.

```
/api/students?department=IT
/api/products?category=mobile
/api/students?page=1&limit=10
```

Convention 5: Return meaningful HTTP status codes.

```
200 OK
201 Created
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
500 Internal Server Error
```

Convention 6: Keep response structures consistent.

Example:

```
{
    "success": true,
    "message": "Students fetched successfully",
    "data": []
}
```

### 10.8 Build a simple REST API

Let's combine these concepts into a small Employee Management API.

Project structure

```
23_REST_API_Fundamentals/
│
├── routes/
│   └── employeeRoutes.js
│
├── controllers/
│   └── employeeController.js
│
├── server.js
│
└── package.json
```

1\. `controllers/employeeController.js`

```
// Temporary employee data
let employees = [

    {
        id: 1,
        name: "Ramesh",
        department: "Development"
    },

    {
        id: 2,
        name: "Suresh",
        department: "Testing"
    }

];

// GET - All employees
const getEmployees = (req, res) => {

    res.status(200).json({

        success: true,

        data: employees

    });

};

// GET - Single employee
const getEmployeeById = (req, res) => {

    const id = Number(req.params.id);

    const employee = employees.find(
        (employee) => employee.id === id
    );

    if (!employee) {

        return res.status(404).json({

            success: false,

            message: "Employee not found"

        });

    }

    res.status(200).json({

        success: true,

        data: employee

    });

};

// POST - Create employee
const createEmployee = (req, res) => {

    const { name, department } = req.body;

    if (!name || !department) {

        return res.status(400).json({

            success: false,

            message: "Name and department are required"

        });

    }

    const newEmployee = {

        id: employees.length
            ? Math.max(...employees.map(employee => employee.id)) + 1
            : 1,

        name,

        department

    };

    employees.push(newEmployee);

    res.status(201).json({

        success: true,

        message: "Employee created successfully",

        data: newEmployee

    });

};

// PUT - Update employee
const updateEmployee = (req, res) => {

    const id = Number(req.params.id);

    const employee = employees.find(
        (employee) => employee.id === id
    );

    if (!employee) {

        return res.status(404).json({

            success: false,

            message: "Employee not found"

        });

    }

    const { name, department } = req.body;

    if (!name || !department) {

        return res.status(400).json({

            success: false,

            message: "Name and department are required"

        });

    }

    employee.name = name;

    employee.department = department;

    res.status(200).json({

        success: true,

        message: "Employee updated successfully",

        data: employee

    });

};

// DELETE - Employee
const deleteEmployee = (req, res) => {

    const id = Number(req.params.id);

    const index = employees.findIndex(
        (employee) => employee.id === id
    );

    if (index === -1) {

        return res.status(404).json({

            success: false,

            message: "Employee not found"

        });

    }

    const deletedEmployee = employees.splice(index, 1)[0];

    res.status(200).json({

        success: true,

        message: "Employee deleted successfully",

        data: deletedEmployee

    });

};

module.exports = {

    getEmployees,

    getEmployeeById,

    createEmployee,

    updateEmployee,

    deleteEmployee

};
```

2\. `routes/employeeRoutes.js`

```
const express = require("express");

const router = express.Router();

const {

    getEmployees,

    getEmployeeById,

    createEmployee,

    updateEmployee,

    deleteEmployee

} = require("../controllers/employeeController");

// GET all employees
router.get("/", getEmployees);

// GET one employee
router.get("/:id", getEmployeeById);

// POST employee
router.post("/", createEmployee);

// PUT employee
router.put("/:id", updateEmployee);

// DELETE employee
router.delete("/:id", deleteEmployee);

module.exports = router;
```

3\. `server.js`

```
const express = require("express");

const app = express();

// Parse JSON
app.use(express.json());

// Import employee router
const employeeRoutes = require("./routes/employeeRoutes");

// Register router
app.use("/api/employees", employeeRoutes);

// Start server
app.listen(3000, () => {

    console.log("REST API running on port 3000");

});
```

### 10.9 Test using Postman

| Method | URL                | Operation |
| ------ | ------------------ | --------- |
| GET    | `/api/employees`   | Read all  |
| GET    | `/api/employees/1` | Read one  |
| POST   | `/api/employees`   | Create    |
| PUT    | `/api/employees/1` | Update    |
| DELETE | `/api/employees/1` | Delete    |

POST body:

```
{
    "name": "Kiran",
    "department": "Development"
}
```

PUT body:

```
{
    "name": "Ramesh Kumar",
    "department": "Backend"
}
```

Note: This example stores data in an array. Restarting the server will reset the data. Later, we will use a database for permanent storage.

## 11. Common mistakes

### Mistake 1 — Using verbs in REST URLs

Avoid:

```
/api/getStudents
/api/createStudent
```

Prefer:

```
GET  /api/students
POST /api/students
```

### Mistake 2 — Using GET to create data

Wrong:

```
app.get("/api/students/create", (req, res) => {
    // Create student
});
```

Correct:

```
app.post("/api/students", (req, res) => {
    // Create student
});
```

### Mistake 3 — Forgetting JSON middleware

Wrong:

```
app.post("/api/students", (req, res) => {

    console.log(req.body);

});
```

Correct:

```
app.use(express.json());

app.post("/api/students", (req, res) => {

    console.log(req.body);

});
```

### Mistake 4 — Returning incorrect status codes

Wrong:

```
res.status(200).json({
    message: "Student created"
});
```

Better:

```
res.status(201).json({
    message: "Student created"
});
```

`201 Created` communicates that a new resource was successfully created.

### Mistake 5 — Ignoring missing resources

Wrong:

```
const student = students.find(
    (student) => student.id === id
);

res.json(student);
```

Better:

```
if (!student) {

    return res.status(404).json({
        message: "Student not found"
    });

}
```

### Mistake 6 — Thinking stateless means no database

REST statelessness does not prevent storing application data in a database. It means the server should not depend on stored client session state to understand each request.

## 12. Best practices

1. Use resource-based URLs.
2. Use HTTP methods correctly.
3. Use plural resource names.
4. Use meaningful HTTP status codes.
5. Return consistent JSON responses.
6. Validate request data.
7. Handle errors properly.
8. Keep route, controller, and business logic organized.
9. Use authentication for protected resources.
10. Use pagination for large collections.
11. Use filtering and sorting where needed.
12. Keep API documentation updated.

### Recommended REST API project structure

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
├── routes/
│   ├── studentRoutes.js
│   └── employeeRoutes.js
│
├── models/
│   ├── Student.js
│   └── Employee.js
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

```
23_REST_API_Fundamentals/
│
├── images/
│   ├── rest-api-architecture.png
│   ├── http-methods.png
│   └── crud-flow.png
│
└── README.md
```

Use actual images committed to your GitHub repository:

```
![REST API Architecture](./images/rest-api-architecture.png)

![HTTP Methods](./images/http-methods.png)

![CRUD Flow](./images/crud-flow.png)
```

The Mermaid diagrams in this chapter can be added directly to README without generating image files.

## 13. Interview questions

### Beginner level

Q1. What is REST?

REST is an architectural style used to design web APIs using standard communication methods such as HTTP.

Q2. What is a REST API?

A REST API is an API designed using REST principles to allow clients and servers to communicate.

Q3. What is a resource?

A resource is an entity managed by an API, such as a student, employee, product, or order.

Q4. What is an endpoint?

An endpoint is a URL used to access a resource or perform an operation.

Q5. What is JSON?

JSON stands for JavaScript Object Notation. It is a lightweight format for exchanging data.

### Intermediate level

Q6. What is the difference between GET and POST?

- GET retrieves data.
- POST submits data, commonly to create a resource.

Q7. What is the difference between PUT and PATCH?

- PUT generally replaces the resource representation.
- PATCH applies partial modifications.

Q8. What is CRUD?

CRUD stands for Create, Read, Update, and Delete.

Q9. What is stateless architecture?

Each request contains the information needed for the server to process it. The server does not rely on remembering client session state between requests.

Q10. Why do we use HTTP status codes?

They communicate the result of an HTTP request to the client.

### Advanced level

Q11. What are the main REST architectural constraints?

The commonly described REST constraints are:

1. Client-server.
2. Stateless.
3. Cacheable.
4. Uniform interface.
5. Layered system.
6. Code on demand (optional).

Q12. Is every HTTP API a REST API?

No. An API can use HTTP without following REST architectural constraints.

Q13. What is the difference between a resource and an endpoint?

A resource represents the data or entity. An endpoint is the URL used to access or operate on that resource.

Q14. Why is pagination important in REST APIs?

Pagination limits the number of records returned in a single response, improving performance and reducing unnecessary data transfer.

Q15. Can REST APIs be used with React and mobile applications?

Yes. Any client that can communicate using HTTP can consume a REST API.

## 14. Practice problems

### Beginner exercises

1. Explain REST in your own words.
2. Identify resources in a library management application.
3. Create GET and POST endpoints for students.
4. Create a JSON response for employee details.
5. Explain the difference between an endpoint and a resource.

### Intermediate exercises

6. Create all CRUD endpoints for products.
7. Create a REST API for customers.
8. Use route parameters to retrieve one employee.
9. Use query parameters to filter products.
10. Return appropriate HTTP status codes.

### Advanced exercises

11. Build a REST API for an online shopping application.
12. Implement pagination for products.
13. Implement filtering and sorting.
14. Create consistent success and error response formats.
15. Design REST endpoints for a complete Library Management System.

## 15. Mini challenge — Book Management REST API

Your task

Build a Book Management REST API.

### Requirements

Create these endpoints:

```
POST    /api/books
GET     /api/books
GET     /api/books/:id
PUT     /api/books/:id
PATCH   /api/books/:id
DELETE  /api/books/:id
```

### Book fields

```
{
    "title": "Python Programming",
    "author": "Ramesh",
    "price": 500,
    "category": "Programming"
}
```

### Expected project structure

```
23_REST_API_Fundamentals/
│
├── controllers/
│   └── bookController.js
│
├── routes/
│   └── bookRoutes.js
│
├── server.js
│
└── package.json
```

### Your task

Implement:

1. Create book.
2. Get all books.
3. Get book by ID.
4. Replace book using PUT.
5. Partially update book using PATCH.
6. Delete book.
7. Validate required fields.
8. Handle missing book IDs.

### Think before coding

For each endpoint, ask yourself:

```
What is the HTTP method?
          ↓
What is the endpoint?
          ↓
What data do I need?
          ↓
What operation should happen?
          ↓
What status code should I return?
          ↓
What JSON response should I send?
```

Try completing this challenge independently before moving forward.

## 16. Chapter summary

| Topic                | What you learned                   |
| -------------------- | ---------------------------------- |
| REST                 | Architectural style for APIs       |
| Resource             | Entity managed by an API           |
| Endpoint             | URL used to access a resource      |
| HTTP methods         | GET, POST, PUT, PATCH, DELETE      |
| CRUD                 | Create, Read, Update, Delete       |
| Stateless            | Requests are handled independently |
| JSON API             | Exchanges JSON data                |
| REST conventions     | Resource-based URL design          |
| Status codes         | Communicate request results        |
| REST API development | Building APIs with Express         |

Main concept: REST provides a standard way to design APIs so frontend applications, mobile applications, and other clients can communicate with backend servers.

## 17. Quick revision

🧠 Remember these important points

- REST stands for Representational State Transfer.
- REST is an architectural style.
- Resources represent application data.
- Endpoints are URLs used to access resources.
- GET reads data.
- POST creates data.
- PUT replaces a resource.
- PATCH partially updates a resource.
- DELETE removes a resource.
- CRUD means Create, Read, Update, Delete.
- Stateless means each request carries the information needed for processing.
- JSON is commonly used for API communication.

  ⭐ Most important REST API structure

| Method | Endpoint         | Operation      |
| ------ | ---------------- | -------------- |
| POST   | `/api/books`     | Create         |
| GET    | `/api/books`     | Read all       |
| GET    | `/api/books/:id` | Read one       |
| PUT    | `/api/books/:id` | Replace        |
| PATCH  | `/api/books/:id` | Partial update |
| DELETE | `/api/books/:id` | Delete         |

Chapter 23 completed

Practice: Build the Book Management REST API mini challenge.

When you're ready, type `NEXT` to start Chapter 24 — CRUD API, where we will build a complete API with Create, Read, Update, Delete, validation, and error handling.