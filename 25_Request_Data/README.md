# 📘 Chapter 25 — Express.js Request Data



PART 5 — EXPRESS.JS

Chapter 25



In this chapter, you will learn how to receive data from the client (React, Postman, browser, etc.) using Express.js.

We will learn five important request properties:

1. `req.params`
2. `req.query`
3. `req.body`
4. `req.headers`
5. `req.cookies`

## 🔑 Requires Before Starting

Before starting this chapter, you should understand:

- Basic JavaScript
- Node.js and Express.js
- Express routes (`GET`, `POST`, `PUT`, `DELETE`)
- Middleware
- Postman basics
- JSON data

Example: When a user sends a request from React to your Express backend, Express needs to read the data sent by that user.

## 📖 Interactive reading

📖 Read — What will you learn?

💡 Important — Remember this

## 1. What is Request Data?

Request data means information sent by a client to a server.

For example, imagine a student registration application.

A user enters:

```
{
  "name": "Ramesh",
  "email": "ramesh@gmail.com",
  "age": 25
}
```

The React frontend sends this information to the Express backend.

Express receives the request and reads the information using request properties.

```
React Frontend
      |
      | HTTP Request
      v
Express Backend
      |
      | Reads request data
      v
req.params
req.query
req.body
req.headers
req.cookies
      |
      v
Controller / Database
```

Simple definition: Request properties help Express read information sent by the client.

## 2. Why do we need Request Data?

Suppose you are building a Student Management System.

You need to perform different operations:

| Requirement                    | Request property |
| ------------------------------ | ---------------- |
| Get a particular student by ID | `req.params`     |
| Search students by department  | `req.query`      |
| Register a new student         | `req.body`       |
| Read an authorization token    | `req.headers`    |
| Read a login session cookie    | `req.cookies`    |

Without request data, your backend cannot properly understand what information the client is sending.

## 3. Real-world analogy

Imagine a courier service.

| Express property | Real-world example                      |
| ---------------- | --------------------------------------- |
| `req.params`     | Parcel tracking number                  |
| `req.query`      | Search or delivery preferences          |
| `req.body`       | Information inside the parcel form      |
| `req.headers`    | Parcel labels and delivery instructions |
| `req.cookies`    | A saved identification/session token    |

For example, when you track a parcel using tracking number `1001`, the tracking number identifies the specific parcel.

Similarly:

```
GET /api/students/1001
```

Here, `1001` is a route parameter.

## 4. Architecture / Flow

[Demystifying HTTP: Request, Response, Headers, Params, Cookies, Query, and Authentication](https://images.openai.com/static-rsc-4/nxDD-JLmnbuiP2PJZVcMkjh2e0G-czqJuyhPFIkohRzbUONV-sMwG5z2xmKFaRFVA8CPrHP-97rT1QYH6aP6jNUUlsCa_-QIi2CU1zsNn3xyoO-vFys7sML0zt0rpBHgMJuKCs1E2O80kE7sQxqJ5znpDVAE2GFbiJTTDKooEIY?purpose=inline)

[linkedin.com](https://www.linkedin.com/pulse/demystifying-http-request-response-headers-params-query-vithanage-p0p3e?utm_source=chatgpt.com)

### Request flow

\#chatgpt-mermaid-\_r_7mi\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_7mi\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_7mi\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_7mi\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_7mi\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_7mi\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_7mi\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_7mi\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_7mi\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_7mi\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_7mi\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_7mi\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_7mi\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_7mi\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_7mi\_ p{margin:0;}#chatgpt-mermaid-\_r_7mi\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_7mi\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_7mi\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_7mi\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_7mi\_ .label text,#chatgpt-mermaid-\_r_7mi\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_7mi\_ .node rect,#chatgpt-mermaid-\_r_7mi\_ .node circle,#chatgpt-mermaid-\_r_7mi\_ .node ellipse,#chatgpt-mermaid-\_r_7mi\_ .node polygon,#chatgpt-mermaid-\_r_7mi\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_7mi\_ .rough-node .label text,#chatgpt-mermaid-\_r_7mi\_ .node .label text,#chatgpt-mermaid-\_r_7mi\_ .image-shape .label,#chatgpt-mermaid-\_r_7mi\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_7mi\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_7mi\_ .rough-node .label,#chatgpt-mermaid-\_r_7mi\_ .node .label,#chatgpt-mermaid-\_r_7mi\_ .image-shape .label,#chatgpt-mermaid-\_r_7mi\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_7mi\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_7mi\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_7mi\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_7mi\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_7mi\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_7mi\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_7mi\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_7mi\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_7mi\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_7mi\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_7mi\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_7mi\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_7mi\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_7mi\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_7mi\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_7mi\_ .icon-shape,#chatgpt-mermaid-\_r_7mi\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_7mi\_ .icon-shape p,#chatgpt-mermaid-\_r_7mi\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_7mi\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_7mi\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_7mi\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_7mi\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_7mi\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_7mi\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_7mi\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_7mi\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_7mi\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_7mi\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_7mi\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_7mi\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_7mi\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_7mi\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_7mi\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_7mi\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_7mi\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_7mi\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_7mi\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_7mi\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_7mi\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_7mi\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_7mi\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_7mi\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_7mi\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_7mi\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_7mi\_ .node rect,#chatgpt-mermaid-\_r_7mi\_ .node circle,#chatgpt-mermaid-\_r_7mi\_ .node ellipse,#chatgpt-mermaid-\_r_7mi\_ .node polygon,#chatgpt-mermaid-\_r_7mi\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_7mi\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_7mi\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_7mi\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_7mi\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_7mi\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}React / Postman ClientHTTP RequestExpress MiddlewareRead Request Datareq.paramsreq.queryreq.bodyreq.headersreq.cookiesRoute / ControllerDatabase / Business LogicHTTP Response

The request reaches Express first. Middleware processes the request, and then your route or controller reads the required data.

## 5. Syntax

Let's understand the five request properties.

### A. `req.params`

Used to read values from the URL path.

Example URL:

```
GET /api/students/101
```

Route:

```
app.get("/api/students/:id", (req, res) => {

    // Read route parameter
    const studentId = req.params.id;

    res.json({
        id: studentId
    });
});
```

Here:

```
req.params.id
```

Output:

```
{
  "id": "101"
}
```

Notice that the value is a string.

You can convert it into a number:

```
const studentId = Number(req.params.id);
```

### B. `req.query`

Used to read query parameters from the URL.

Example URL:

```
GET /api/students?department=IT&age=25
```

Route:

```
app.get("/api/students", (req, res) => {

    // Read query parameters
    const department = req.query.department;
    const age = req.query.age;

    res.json({
        department: department,
        age: age
    });
});
```

Output:

```
{
  "department": "IT",
  "age": "25"
}
```

Common uses:

- Search
- Filtering
- Sorting
- Pagination

Example:

```
/api/students?page=1&limit=10
```

### C. `req.body`

Used to read data sent inside the request body.

Usually used with:

- POST
- PUT
- PATCH

First, add JSON middleware:

```
app.use(express.json());
```

Then:

```
app.post("/api/students", (req, res) => {

    // Read request body
    const student = req.body;

    res.json({
        message: "Student received",
        data: student
    });
});
```

Send this JSON from Postman:

```
{
  "name": "Ramesh",
  "email": "ramesh@gmail.com",
  "age": 25
}
```

Output:

```
{
  "message": "Student received",
  "data": {
    "name": "Ramesh",
    "email": "ramesh@gmail.com",
    "age": 25
  }
}
```

Important: Without `express.json()` middleware, Express will not automatically parse incoming JSON request bodies.

### D. `req.headers`

Headers contain additional information about an HTTP request.

Example:

```
Authorization: Bearer your-token
Content-Type: application/json
Accept: application/json
```

Read headers:

```
app.get("/api/profile", (req, res) => {

    // Read authorization header
    const authorization = req.headers.authorization;

    // Read content type
    const contentType = req.headers["content-type"];

    res.json({
        authorization: authorization,
        contentType: contentType
    });
});
```

You can also use:

```
const authorization = req.get("Authorization");
```

Common uses:

- Authentication
- Content type
- Accepted response formats
- Client information

Never expose or log real authentication tokens unnecessarily.

### E. `req.cookies`

Cookies are small pieces of data stored by the browser and sent with matching requests.

Example:

```
Cookie: sessionId=abc123
```

Express does not automatically parse cookies into `req.cookies`.

First install the package:

```
npm install cookie-parser
```

Import and configure it:

```
const cookieParser = require("cookie-parser");

// Register cookie middleware
app.use(cookieParser());
```

Now read cookies:

```
app.get("/api/profile", (req, res) => {

    // Read cookie
    const sessionId = req.cookies.sessionId;

    res.json({
        sessionId: sessionId
    });
});
```

Setting a cookie:

```
app.get("/set-cookie", (req, res) => {

    // Create a cookie
    res.cookie("username", "Ramesh", {
        httpOnly: true,
        secure: process.env.NODE_ENV === "production",
        sameSite: "lax"
    });

    res.json({
        message: "Cookie created"
    });
});
```

Clearing a cookie:

```
app.get("/clear-cookie", (req, res) => {

    // Remove the cookie
    res.clearCookie("username");

    res.json({
        message: "Cookie cleared"
    });
});
```

`cookie-parser` is needed for reading cookies through `req.cookies`. Express itself provides `res.cookie()` and `res.clearCookie()`.

For production authentication, use secure session or token patterns. Cookie options such as `HttpOnly`, `Secure`, and `SameSite` are important.

## 6. Basic Example

Let's understand all five properties in one small Express application.

### Project structure

```
25_Request_Data/
│
├── server.js
├── package.json
└── .env
```

### Install packages

```
npm init -y
npm install express cookie-parser
npm install --save-dev nodemon
```

### server.js

```
// Import Express
const express = require("express");

// Import cookie-parser
const cookieParser = require("cookie-parser");

// Create Express application
const app = express();

// Parse JSON request bodies
app.use(express.json());

// Parse URL-encoded form data
app.use(express.urlencoded({ extended: true }));

// Parse cookies
app.use(cookieParser());

// ----------------------------------
// 1. req.params
// ----------------------------------

app.get("/api/students/:id", (req, res) => {

    const id = req.params.id;

    res.json({
        message: "Student ID received",
        studentId: id
    });
});

// ----------------------------------
// 2. req.query
// ----------------------------------

app.get("/api/search", (req, res) => {

    const department = req.query.department;
    const page = Number(req.query.page || 1);

    res.json({
        department: department,
        page: page
    });
});

// ----------------------------------
// 3. req.body
// ----------------------------------

app.post("/api/students", (req, res) => {

    const { name, email, age } = req.body;

    res.status(201).json({
        message: "Student data received",
        student: {
            name,
            email,
            age
        }
    });
});

// ----------------------------------
// 4. req.headers
// ----------------------------------

app.get("/api/headers", (req, res) => {

    const authorization = req.get("Authorization");

    res.json({
        authorization: authorization || null
    });
});

// ----------------------------------
// 5. req.cookies
// ----------------------------------

app.get("/api/cookies", (req, res) => {

    const username = req.cookies.username;

    res.json({
        username: username || null
    });
});

// Create cookie
app.get("/set-cookie", (req, res) => {

    res.cookie("username", "Ramesh", {
        httpOnly: true,
        sameSite: "lax"
    });

    res.json({
        message: "Cookie created"
    });
});

// Start server
app.listen(3000, () => {
    console.log("Server running on port 3000");
});
```

Run the application:

```
node server.js
```

Or use Nodemon:

```
npx nodemon server.js
```

## 7. Dry Run

Let's understand how Express reads each request.

### Example 1 — `req.params`

Request:

```
GET http://localhost:3000/api/students/101
```

Express reads:

```
req.params.id
```

Step-by-step:

```
URL: /api/students/101
          |
          v
Route: /api/students/:id
          |
          v
id = "101"
          |
          v
Send JSON response
```

### Example 2 — `req.query`

Request:

```
GET http://localhost:3000/api/search?department=IT&page=2
```

Express reads:

```
req.query.department
req.query.page
```

Values:

```
department = "IT"
page = "2"
```

### Example 3 — `req.body`

Request:

```
POST http://localhost:3000/api/students
```

Body:

```
{
  "name": "Ramesh",
  "email": "ramesh@gmail.com",
  "age": 25
}
```

Express reads:

```
req.body.name
req.body.email
req.body.age
```

### Example 4 — `req.headers`

Request header:

```
Authorization: Bearer demo-token
```

Express reads:

```
req.get("Authorization")
```

### Example 5 — `req.cookies`

First request:

```
GET http://localhost:3000/set-cookie
```

Server sends a cookie.

Next request:

```
GET http://localhost:3000/api/cookies
```

Browser or cookie-enabled client sends the cookie back. Express reads it using:

```
req.cookies.username
```

## 8. Output

Here are the expected outputs.

| Request                                | Expected result               |
| -------------------------------------- | ----------------------------- |
| `GET /api/students/101`                | Student ID: `"101"`           |
| `GET /api/search?department=IT&page=2` | Department: `"IT"`, page: `2` |
| `POST /api/students`                   | Student information           |
| `GET /api/headers`                     | Authorization header          |
| `GET /api/cookies`                     | Username cookie or `null`     |

Example response:

```
{
  "message": "Student ID received",
  "studentId": "101"
}
```

## 9. Line-by-line explanation

Let's understand the most important lines.

1\. Import Express

```
const express = require("express");
```

Loads the Express package into your application.

2\. Create an Express application

```
const app = express();
```

Creates the application instance. You use `app` to configure middleware and routes.

3\. Parse JSON

```
app.use(express.json());
```

Reads JSON request bodies and makes the parsed data available through `req.body`.

4\. Parse cookies

```
app.use(cookieParser());
```

Reads cookies sent by the client and makes them available through `req.cookies`.

5\. Read route parameters

```
const id = req.params.id;
```

Reads the `id` value from the URL path.

6\. Read query parameters

```
const page = req.query.page;
```

Reads the `page` value from the URL query string.

7\. Read body data

```
const name = req.body.name;
```

Reads the `name` property from the request body.

8\. Read headers

```
const token = req.get("Authorization");
```

Reads the Authorization header.

9\. Read cookies

```
const username = req.cookies.username;
```

Reads the `username` cookie parsed by `cookie-parser`.

## 10. Practical Example — Student Management API

Let's compare all five request properties.

| Property      | Example                       | When should you use it?                 |
| ------------- | ----------------------------- | --------------------------------------- |
| `req.params`  | `/students/101`               | Identify a specific student             |
| `req.query`   | `/students?department=IT`     | Filter or search students               |
| `req.body`    | `{ "name": "Ramesh" }`        | Create or update student data           |
| `req.headers` | `Authorization: Bearer token` | Read authentication or request metadata |
| `req.cookies` | `username=Ramesh`             | Read browser cookie/session information |

### One practical route using multiple properties

```
app.get("/api/students/:id", (req, res) => {

    // 1. Read student ID from URL path
    const id = Number(req.params.id);

    // 2. Read includeMarks from query string
    const includeMarks = req.query.includeMarks === "true";

    // 3. Read optional authorization header
    const authorization = req.get("Authorization");

    // 4. Read username cookie
    const username = req.cookies.username;

    // Send response
    res.json({
        studentId: id,
        includeMarks: includeMarks,
        hasAuthorization: Boolean(authorization),
        username: username || null
    });
});
```

Request:

```
GET http://localhost:3000/api/students/101?includeMarks=true
```

Possible response:

```
{
  "studentId": 101,
  "includeMarks": true,
  "hasAuthorization": false,
  "username": null
}
```

Here we used four request properties in one route. The body is not needed for this GET request.

### Test using Postman

[Mastering API Testing with Postman: A Complete Guide for Developers](https://images.openai.com/static-rsc-4/sGRFCAAanc0zJNhTO3S1brsIdtHdQy-lRmrijURgaVQ-RQYlHhAiLAmTLmwatjjIzInaEI4qmnHaKqRVY27QLVKfkxWwX19G6MuwstrQTZOgWW4LzUC_02RfRVd26s6dMfnc6Ed_Vu52gAuYCKbvPKyHy6q8etPX9d2HPEkFAt8?purpose=inline)

[Authorization Bearer Token Example](https://images.openai.com/static-rsc-4/mBTJl784W7g9bNiU5vOyIGdy5GtLqmHZjjHY_vElxZtMwkV_U1xm01EYTtxHm7AN_1bDXJLsXPHpAt2GLNXNxvWnoMrWwRWV5eqlDT2NxHFI4uxJohi289Y9T1yR6fRtakNrBfjRM9xyZxUe64SNHb7AIkzMvDrhF4feu8PYAUw?purpose=inline)

[Postman - POST Requests](https://images.openai.com/static-rsc-4/UQI52XlIjZT9C_hCLz3M0DBvY6Kenutsqcqsj3asckYbvg3MgLsk5oxqBC1onodAfngDjOyJPaDMpDKbYBy5Rd53aK0Mgr_4jRXz3yQQM5d6llgy4cMucPHD_329HGX4TyY9Ua9tNM2tAQUxu_aiEsLs7Hm9JdGv-6GGOZc8iuk?purpose=inline)

1. Select the HTTP method.
2. Enter the API URL.
3. For `req.params`, enter the ID in the URL.
4. For `req.query`, use the Params tab.
5. For `req.body`, select Body → raw → JSON.
6. For `req.headers`, use the Headers tab.
7. For `req.cookies`, use the Cookies manager or a client that sends cookies.

Important: When making cross-origin browser requests with cookies, the client must send credentials and the server's CORS configuration must allow credentials for the trusted origin.

## 11. Common mistakes

| Mistake                                   | Correct approach                      |
| ----------------------------------------- | ------------------------------------- |
| Using `req.param` instead of `req.params` | Use `req.params`                      |
| Reading JSON without middleware           | Add `express.json()`                  |
| Assuming query values are numbers         | Convert and validate them             |
| Assuming cookies are automatically parsed | Install and register `cookie-parser`  |
| Using `req.body` for URL path IDs         | Use `req.params`                      |
| Putting large data in URL query strings   | Send appropriate data in request body |
| Exposing authentication tokens            | Avoid exposing or logging secrets     |
| Trusting client input                     | Validate all incoming data            |

## 12. Best practices

1. Use `req.params` for resource identifiers.
2. Use `req.query` for filters, search, sorting, and pagination.
3. Use `req.body` for submitted data.
4. Use `req.headers` for metadata and authentication information.
5. Use `req.cookies` for cookie-based session information.
6. Validate every value received from the client.
7. Convert strings into numbers or booleans when needed.
8. Use secure cookie settings for production.
9. Never trust incoming data automatically.
10. Keep request parsing middleware before the routes that need it.

### Middleware execution order

```
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.use(cookieParser());

// Routes should come after these middleware functions.
app.use("/api/students", studentRoutes);
```

## 13. Interview questions

Q1. What is `req.params`?

It reads values from the URL path.

Example: `/students/101`.

Q2. What is `req.query`?

It reads values from the URL query string.

Example: `/students?page=1`.

Q3. What is `req.body`?

It reads data sent inside the HTTP request body.

Q4. Why do we use `express.json()`?

To parse incoming JSON request bodies.

Q5. What is `req.headers`?

It reads request metadata such as Authorization and Content-Type.

Q6. What is `req.cookies`?

It reads cookies sent by the client after cookie-parsing middleware is configured.

Q7. Does Express automatically parse cookies?

No. A package such as `cookie-parser` is commonly used.

Q8. What is the difference between params and query?

- Params identify a resource.
- Query parameters filter, search, sort, or paginate resources.

Q9. Are route parameters and query parameters strings?

Usually yes. Convert and validate them when you need numbers or other types.

Q10. What is the difference between `req.body` and `req.headers`?

- Body contains submitted request data.
- Headers contain request metadata and instructions.

## 14. Practice problems

Try these exercises in VS Code and Postman.

Exercise 1 — Route Parameters

Create this API:

```
GET /api/books/:id
```

Read the book ID using `req.params`.

Exercise 2 — Query Parameters

Create this API:

```
GET /api/products?category=mobile
```

Read the category using `req.query`.

Exercise 3 — Request Body

Create this API:

```
POST /api/users
```

Receive name, email, and password using `req.body`. Do not return the password in the response.

Exercise 4 — Headers

Create this API:

```
GET /api/profile
```

Read the Authorization header.

Exercise 5 — Cookies

Create APIs to set, read, and clear a username cookie.

## 15. Mini Challenge — Student API

Your task

Build an API that uses all five request properties.

Requirements:

1. Read student ID from `req.params`.
2. Read department from `req.query`.
3. Receive student details using `req.body`.
4. Read Authorization from `req.headers`.
5. Read username from `req.cookies`.

Expected API design:

| Method | Endpoint                      | Purpose                |
| ------ | ----------------------------- | ---------------------- |
| GET    | `/api/students/:id`           | Read student ID        |
| GET    | `/api/students?department=IT` | Filter students        |
| POST   | `/api/students`               | Create student         |
| GET    | `/api/profile`                | Read header and cookie |

### Logic-building exercise

Before writing code, think about these steps:

```
Step 1: What is the input?
Step 2: Where does the input come from?
Step 3: Which req property should I use?
Step 4: How do I validate the input?
Step 5: What response should I send?
```

Try writing the code yourself before checking your notes.

## 16. Chapter summary

You learned five important Express request properties:

1

`req.params`

URL path

Example: `/students/101`

2

`req.query`

URL query

Example: `/students?page=1`

3

`req.body`

Request body

Example: `{ "name": "Ramesh" }`

4

`req.headers`

Request metadata

Example: `Authorization`

5

`req.cookies`

Client cookies

Example: `username=Ramesh`

## 17. Quick revision

Test your understanding.

Chapter 25 Quiz

0/5 answered

1\. Which property reads an ID from /students/101?

req.body

req.params

req.headers



2\. Which middleware parses JSON request bodies?

express.json()

cookieParser()

express.static()



3\. Which property is used for /products?page=2?

req.params

req.query

req.cookies



4\. Which package commonly parses cookies?

mongoose

cookie-parser

nodemon



5\. Which property reads the Authorization header?

req.headers

req.body

req.params



Check my answers

Chapter 25 Completed

You have now completed Express.js Request Data.

Your next chapter in the syllabus is Chapter 26 — Express.js Project Structure and Professional API Organization.

Type NEXT when you are ready.