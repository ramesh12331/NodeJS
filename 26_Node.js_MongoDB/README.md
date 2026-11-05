# 📘 PART 7 — DATABASES

We are starting a new part of the Node.js course. We will follow your updated syllabus.

# Chapter 26 — Node.js + MongoDB



Beginner to Intermediate

Practical Learning



## 📚 Chapter Topics

1. What is MongoDB?
2. SQL vs MongoDB
3. MongoDB basics
4. Collections
5. Documents
6. Installing MongoDB
7. Connecting Node.js with MongoDB
8. MongoDB Driver
9. Introduction to Mongoose
10. Schemas
11. Models
12. Documents in Mongoose
13. CRUD operations
14. MongoDB queries
15. Validation
16. Practical Student Management API
17. Interview questions
18. Practice exercises
19. Chapter summary

## 1. What is MongoDB?

MongoDB is a NoSQL database used to store application data.

It stores data in a document format similar to JSON.

For example, imagine we are building a Student Management Application.

We need to store student information:

- Student name
- Age
- Email
- Course

MongoDB stores this information as a document.

```
{
    "name": "Ramesh",
    "age": 25,
    "email": "ramesh@gmail.com",
    "course": "Node.js"
}
```

Simple definition:

MongoDB is a document-oriented NoSQL database that stores data in flexible, JSON-like documents.

## 2. SQL vs MongoDB

You have already learned PostgreSQL and SQL. Let's compare them with MongoDB.

| SQL Database                  | MongoDB                     |
| ----------------------------- | --------------------------- |
| Relational database           | NoSQL database              |
| Tables                        | Collections                 |
| Rows                          | Documents                   |
| Columns                       | Fields                      |
| SQL queries                   | MongoDB queries             |
| Usually fixed table structure | Flexible document structure |
| PostgreSQL, MySQL             | MongoDB                     |

### Example: Student data in SQL

Students table

| id | name   | age | course  |
| -- | ------ | --- | ------- |
| 1  | Ramesh | 25  | Node.js |
| 2  | Kiran  | 23  | React   |

### Same data in MongoDB

students collection

```
[
    {
        "_id": "student1",
        "name": "Ramesh",
        "age": 25,
        "course": "Node.js"
    },
    {
        "_id": "student2",
        "name": "Kiran",
        "age": 23,
        "course": "React"
    }
]
```

### Remember this relationship

```
SQL                         MongoDB

Database                    Database
   |                           |
   v                           v
Table                       Collection
   |                           |
   v                           v
Row                         Document
   |                           |
   v                           v
Column                      Field
```

## 3. MongoDB Basics

There are three important concepts:

1. Database
2. Collection
3. Document

Let's understand each one.

### 3.1 Database

A database is a container that holds collections.

Example:

```
collegeDB
```

Inside this database, we can create collections such as:

```
collegeDB
    |
    |---- students
    |
    |---- teachers
    |
    |---- courses
    |
    |---- employees
```

### 3.2 Collection

A collection is a group of related documents.

For example:

```
students collection
```

It stores student information.

### 3.3 Document

A document is an individual record inside a collection.

Example:

```
{
    "_id": 1,
    "name": "Ramesh",
    "age": 25,
    "course": "Node.js"
}
```

Another document:

```
{
    "_id": 2,
    "name": "Kiran",
    "age": 23,
    "course": "React"
}
```

### Quick understanding

| Concept    | Example             |
| ---------- | ------------------- |
| Database   | collegeDB           |
| Collection | students            |
| Document   | One student record  |
| Field      | name, age, course   |
| Value      | Ramesh, 25, Node.js |

## 4. Installing MongoDB

MongoDB can be used locally or through a cloud service.

### Option 1: MongoDB Community Server

Download MongoDB Community Server:

[Download MongoDB Community Server](https://www.mongodb.com/try/download/community?utm_source=chatgpt.com)

This allows you to run MongoDB on your computer.

### Option 2: MongoDB Atlas

MongoDB Atlas is a cloud database service.

You can create a database without installing the MongoDB server locally.

[Open MongoDB Atlas](https://www.mongodb.com/cloud/atlas?utm_source=chatgpt.com)

[Tutorial Express Parte 3: Usando um banco de dados (com Mongoose) - Aprendendo desenvolvimento web | MDN](https://images.openai.com/static-rsc-4/4-2UX-fb_Zy4o4nftCT-9vwAGJpIVwmg_pnHPdR5k7eXSxU5d1ctGG26tLbHMDdrXHW7SD3RZ3ScEngHiZcFcl5oJRhUiCvhgEDMq_0HY0Ojw-RKN2hDCHdsywmYYuMK2_xW59Nu7PeU7JW-wCZif6xB2bNtnGlu9_o8Uxr5UOA?purpose=inline)

[developer.mozilla.org](https://developer.mozilla.org/pt-BR/docs/Learn_web_development/Extensions/Server-side/Express_Nodejs/mongoose?utm_source=chatgpt.com)

For this course: You can use MongoDB Atlas or a local MongoDB server. The Node.js code is almost the same; only the connection URL changes.

## 5. Connecting Node.js with MongoDB

Let's create a simple Node.js project.

### Step 1: Create project

Open VS Code terminal:

```
mkdir mongodb-practice
cd mongodb-practice
npm init -y
```

### Step 2: Install MongoDB Driver

```
npm install mongodb
```

The `mongodb` package is the official MongoDB Node.js Driver.

### Step 3: Project structure

```
mongodb-practice/
│
├── node_modules/
│
├── package.json
│
├── .env
│
└── server.js
```

### Step 4: Create `.env`

For a local MongoDB server:

```
MONGO_URI=mongodb://127.0.0.1:27017
```

For MongoDB Atlas, use the connection string provided by Atlas:

```
MONGO_URI=mongodb+srv://<username>:<password>@<cluster-url>/
```

Replace the placeholders with your actual database credentials. Never share your real connection string publicly.

### Step 5: Install dotenv

```
npm install dotenv
```

### Step 6: Connect using MongoDB Driver

Create `server.js`:

```
// Import MongoDB package
const { MongoClient } = require("mongodb");

// Load environment variables
require("dotenv").config();

// Get MongoDB connection URL
const url = process.env.MONGO_URI;

// Create MongoDB client
const client = new MongoClient(url);

// Connect to MongoDB
async function connectDB() {

    try {

        // Connect to MongoDB server
        await client.connect();

        console.log("MongoDB connected successfully");

        // Select database
        const db = client.db("collegeDB");

        console.log("Database selected:", db.databaseName);

    } catch (error) {

        console.log("MongoDB connection failed:", error);

    }

}

// Call connection function
connectDB();
```

### Step-by-step explanation

| Code                   | Explanation                      |
| ---------------------- | -------------------------------- |
| `MongoClient`          | Creates a MongoDB client         |
| `new MongoClient(url)` | Creates a connection client      |
| `client.connect()`     | Connects to MongoDB              |
| `client.db()`          | Selects a database               |
| `async`                | Allows asynchronous operations   |
| `await`                | Waits for an operation to finish |
| `try/catch`            | Handles errors                   |

Run:

```
node server.js
```

Expected output:

```
MongoDB connected successfully
Database selected: collegeDB
```

The database may not appear in MongoDB until data is stored in it.

## 6. MongoDB Driver

MongoDB Driver is the official library that allows Node.js applications to communicate directly with MongoDB.

We installed it using:

```
npm install mongodb
```

Import:

```
const { MongoClient } = require("mongodb");
```

### What can we do with the driver?

- Connect to MongoDB.
- Create collections.
- Insert documents.
- Read documents.
- Update documents.
- Delete documents.
- Execute queries.

### Example: Insert one student

```
const { MongoClient } = require("mongodb");

require("dotenv").config();

const client = new MongoClient(process.env.MONGO_URI);

async function insertStudent() {

    try {

        await client.connect();

        const db = client.db("collegeDB");

        const students = db.collection("students");

        // Student data
        const student = {
            name: "Ramesh",
            age: 25,
            course: "Node.js"
        };

        // Insert document
        const result = await students.insertOne(student);

        console.log("Inserted ID:", result.insertedId);

    } catch (error) {

        console.log(error);

    } finally {

        // Close connection
        await client.close();

    }

}

insertStudent();
```

### What happens?

```
Node.js Application
        |
        v
MongoDB Driver
        |
        v
MongoDB Server
        |
        v
collegeDB
        |
        v
students collection
        |
        v
Student document inserted
```

## 7. Introduction to Mongoose

Mongoose is a popular Object Data Modeling (ODM) library for MongoDB and Node.js.

It makes working with MongoDB easier by providing schemas, models, validation and other features.

Install:

```
npm install mongoose
```

Import:

```
const mongoose = require("mongoose");
```

### MongoDB Driver vs Mongoose

| MongoDB Driver                      | Mongoose                   |
| ----------------------------------- | -------------------------- |
| Official MongoDB library            | ODM library                |
| Direct database operations          | Schema-based data modeling |
| No Mongoose schema system           | Supports schemas           |
| Manual validation logic can be used | Built-in schema validation |
| Uses `MongoClient`                  | Uses `mongoose.connect()`  |

### Simple example

MongoDB Driver:

```
const students = db.collection("students");

await students.insertOne({
    name: "Ramesh",
    age: 25
});
```

Mongoose:

```
const student = new Student({
    name: "Ramesh",
    age: 25
});

await student.save();
```

We will use Mongoose for most of our practical Node.js projects.

## 8. Mongoose Connection

Create `server.js`:

```
const mongoose = require("mongoose");

require("dotenv").config();

// Connect to MongoDB
async function connectDB() {

    try {

        await mongoose.connect(process.env.MONGO_URI);

        console.log("MongoDB connected successfully");

    } catch (error) {

        console.log("Database connection failed:", error.message);

        process.exit(1);

    }

}

connectDB();
```

### `.env`

```
MONGO_URI=mongodb://127.0.0.1:27017/collegeDB
```

Notice that the database name is included in this connection URL.

### Important methods

| Method                  | Purpose                       |
| ----------------------- | ----------------------------- |
| `mongoose.connect()`    | Connect to MongoDB            |
| `mongoose.disconnect()` | Disconnect from MongoDB       |
| `mongoose.connection`   | Access connection information |

## 9. What is a Schema?

A Schema defines the structure and rules for documents in a MongoDB collection when using Mongoose.

For example, a student should have:

- Name
- Age
- Email
- Course

Create `models/Student.js`:

```
const mongoose = require("mongoose");

// Create student schema
const studentSchema = new mongoose.Schema({

    name: String,

    age: Number,

    email: String,

    course: String

});

// Export schema as a model
module.exports = mongoose.model("Student", studentSchema);
```

### Schema structure

```
Student Schema
      |
      |---- name     : String
      |
      |---- age      : Number
      |
      |---- email    : String
      |
      |---- course   : String
```

Here:

- `name` is a field.
- `String` is its data type.
- `age` is a field.
- `Number` is its data type.

## 10. What is a Model?

A Model is created from a Mongoose Schema and provides methods to interact with a MongoDB collection.

Example:

```
const mongoose = require("mongoose");

const studentSchema = new mongoose.Schema({
    name: String,
    age: Number
});

// Create model
const Student = mongoose.model("Student", studentSchema);
```

Now we can use the model:

```
await Student.find();

await Student.create({
    name: "Ramesh",
    age: 25
});
```

### Schema vs Model

| Schema                     | Model                        |
| -------------------------- | ---------------------------- |
| Defines document structure | Interacts with collection    |
| Defines fields             | Provides CRUD methods        |
| Defines validation rules   | Executes database operations |

Remember: Schema defines the structure; Model performs database operations.

## 11. What is a Document?

A document is one individual record stored inside a MongoDB collection.

Example:

```
{
    "_id": "673abc123",
    "name": "Ramesh",
    "age": 25,
    "email": "ramesh@gmail.com",
    "course": "Node.js"
}
```

Here:

- `_id` uniquely identifies the document.
- `name`, `age`, `email`, and `course` are fields.

MongoDB automatically generates an `_id` when one is not provided.

## 12. CRUD Operations Using Mongoose

CRUD means:

| Operation | Meaning       | Mongoose method       |
| --------- | ------------- | --------------------- |
| Create    | Insert data   | `create()`            |
| Read      | Retrieve data | `find()`              |
| Update    | Modify data   | `findByIdAndUpdate()` |
| Delete    | Remove data   | `findByIdAndDelete()` |

### Create

```
const newStudent = await Student.create({
    name: "Ramesh",
    age: 25,
    email: "ramesh@gmail.com",
    course: "Node.js"
});

console.log(newStudent);
```

### Read all students

```
const students = await Student.find();

console.log(students);
```

### Read one student

```
const student = await Student.findOne({
    name: "Ramesh"
});

console.log(student);
```

### Read by ID

```
const student = await Student.findById("YOUR_STUDENT_ID");

console.log(student);
```

### Update student

```
const updatedStudent = await Student.findByIdAndUpdate(
    "YOUR_STUDENT_ID",
    {
        age: 26
    },
    {
        new: true,
        runValidators: true
    }
);

console.log(updatedStudent);
```

`new: true` returns the updated document.

`runValidators: true` runs applicable schema validators during this update.

### Delete student

```
const deletedStudent = await Student.findByIdAndDelete(
    "YOUR_STUDENT_ID"
);

console.log(deletedStudent);
```

## 13. MongoDB Queries

Queries help us find documents that match specific conditions.

Imagine our students collection contains:

```
[
    {
        "name": "Ramesh",
        "age": 25,
        "course": "Node.js"
    },
    {
        "name": "Kiran",
        "age": 23,
        "course": "React"
    },
    {
        "name": "Arun",
        "age": 28,
        "course": "Node.js"
    }
]
```

### 13.1 Find all students

```
const students = await Student.find();
```

### 13.2 Find students by course

```
const students = await Student.find({
    course: "Node.js"
});
```

Expected matching students:

```
[
    {
        "name": "Ramesh",
        "age": 25,
        "course": "Node.js"
    },
    {
        "name": "Arun",
        "age": 28,
        "course": "Node.js"
    }
]
```

### 13.3 Find students older than 24

```
const students = await Student.find({
    age: { $gt: 24 }
});
```

### 13.4 Find students younger than 25

```
const students = await Student.find({
    age: { $lt: 25 }
});
```

### 13.5 Find students with age greater than or equal to 25

```
const students = await Student.find({
    age: { $gte: 25 }
});
```

### 13.6 Find students with age between 23 and 26

```
const students = await Student.find({
    age: {
        $gte: 23,
        $lte: 26
    }
});
```

### Important MongoDB operators

| Operator | Meaning                           |
| -------- | --------------------------------- |
| `$eq`    | Equal                             |
| `$ne`    | Not equal                         |
| `$gt`    | Greater than                      |
| `$gte`   | Greater than or equal             |
| `$lt`    | Less than                         |
| `$lte`   | Less than or equal                |
| `$in`    | Matches any value in an array     |
| `$nin`   | Does not match values in an array |

## 14. MongoDB Validation

Validation ensures that documents follow the required data rules.

For example:

- Name is required.
- Email is required.
- Age must be a number.
- Age must be greater than zero.

### Example schema with validation

```
const studentSchema = new mongoose.Schema({

    name: {
        type: String,
        required: true
    },

    age: {
        type: Number,
        required: true,
        min: 1,
        max: 120
    },

    email: {
        type: String,
        required: true
    },

    course: {
        type: String,
        required: true
    }

});
```

Try inserting invalid data:

```
await Student.create({
    name: "",
    age: -10,
    email: "ramesh@gmail.com",
    course: "Node.js"
});
```

The age validation will fail because the age is below the minimum.

Note: `required: true` checks that a value is present. For strings, an empty string is not automatically rejected by every required rule configuration. Use additional validation such as `minLength` or a custom validator when needed.

## 15. Practical Student Management API

Now let's combine Express, MongoDB and Mongoose.

### Project structure

```
student-management/
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
├── .env
├── server.js
└── package.json
```

### Step 1: Install packages

```
npm init -y

npm install express mongoose dotenv
```

### Step 2: `.env`

```
PORT=3000
MONGO_URI=mongodb://127.0.0.1:27017/collegeDB
```

### Step 3: `config/db.js`

```
const mongoose = require("mongoose");

const connectDB = async () => {

    try {

        await mongoose.connect(process.env.MONGO_URI);

        console.log("MongoDB connected successfully");

    } catch (error) {

        console.log("MongoDB error:", error.message);

        process.exit(1);

    }

};

module.exports = connectDB;
```

### Step 4: `models/Student.js`

```
const mongoose = require("mongoose");

const studentSchema = new mongoose.Schema({

    name: {
        type: String,
        required: true,
        trim: true
    },

    age: {
        type: Number,
        required: true,
        min: 1
    },

    email: {
        type: String,
        required: true,
        lowercase: true
    },

    course: {
        type: String,
        required: true,
        trim: true
    }

});

const Student = mongoose.model("Student", studentSchema);

module.exports = Student;
```

### Step 5: `controllers/studentController.js`

```
const Student = require("../models/Student");

// CREATE
const createStudent = async (req, res) => {

    try {

        const student = await Student.create(req.body);

        res.status(201).json({
            message: "Student created successfully",
            data: student
        });

    } catch (error) {

        res.status(400).json({
            message: error.message
        });

    }

};

// READ ALL
const getStudents = async (req, res) => {

    try {

        const students = await Student.find();

        res.status(200).json({
            data: students
        });

    } catch (error) {

        res.status(500).json({
            message: error.message
        });

    }

};

// READ ONE
const getStudentById = async (req, res) => {

    try {

        const student = await Student.findById(req.params.id);

        if (!student) {
            return res.status(404).json({
                message: "Student not found"
            });
        }

        res.status(200).json({
            data: student
        });

    } catch (error) {

        res.status(400).json({
            message: "Invalid student ID"
        });

    }

};

// UPDATE
const updateStudent = async (req, res) => {

    try {

        const student = await Student.findByIdAndUpdate(
            req.params.id,
            req.body,
            {
                new: true,
                runValidators: true
            }
        );

        if (!student) {
            return res.status(404).json({
                message: "Student not found"
            });
        }

        res.status(200).json({
            message: "Student updated successfully",
            data: student
        });

    } catch (error) {

        res.status(400).json({
            message: error.message
        });

    }

};

// DELETE
const deleteStudent = async (req, res) => {

    try {

        const student = await Student.findByIdAndDelete(req.params.id);

        if (!student) {
            return res.status(404).json({
                message: "Student not found"
            });
        }

        res.status(200).json({
            message: "Student deleted successfully"
        });

    } catch (error) {

        res.status(400).json({
            message: "Invalid student ID"
        });

    }

};

module.exports = {
    createStudent,
    getStudents,
    getStudentById,
    updateStudent,
    deleteStudent
};
```

### Step 6: `routes/studentRoutes.js`

```
const express = require("express");

const router = express.Router();

const {
    createStudent,
    getStudents,
    getStudentById,
    updateStudent,
    deleteStudent
} = require("../controllers/studentController");

// CREATE
router.post("/", createStudent);

// READ ALL
router.get("/", getStudents);

// READ ONE
router.get("/:id", getStudentById);

// UPDATE
router.put("/:id", updateStudent);

// DELETE
router.delete("/:id", deleteStudent);

module.exports = router;
```

### Step 7: `server.js`

```
const express = require("express");

require("dotenv").config();

const connectDB = require("./config/db");

const studentRoutes = require("./routes/studentRoutes");

const app = express();

// Middleware
app.use(express.json());

// API routes
app.use("/api/students", studentRoutes);

// Start application after database connects
const startServer = async () => {

    await connectDB();

    app.listen(process.env.PORT || 3000, () => {
        console.log("Server running");
    });

};

startServer();
```

### Step 8: Test using Postman

Create student

POST:

```
http://localhost:3000/api/students
```

Body:

```
{
    "name": "Ramesh",
    "age": 25,
    "email": "ramesh@gmail.com",
    "course": "Node.js"
}
```

Get all students

GET:

```
http://localhost:3000/api/students
```

Get one student

GET:

```
http://localhost:3000/api/students/YOUR_STUDENT_ID
```

Update student

PUT:

```
http://localhost:3000/api/students/YOUR_STUDENT_ID
```

Delete student

DELETE:

```
http://localhost:3000/api/students/YOUR_STUDENT_ID
```

## 16. Interview Questions

## 17. Practice Exercises

- Create a MongoDB database named `companyDB`.
- Create an `employees` collection.
- Insert five employee documents.
- Retrieve all employees.
- Find employees by department.
- Find employees with salary greater than 30000.
- Update an employee's salary.
- Delete an employee.
- Create a Mongoose Employee schema.
- Create CRUD APIs using Express and Mongoose.

## 18. Chapter Summary

| Concept        | Meaning                           |
| -------------- | --------------------------------- |
| MongoDB        | NoSQL database                    |
| Database       | Container for collections         |
| Collection     | Group of documents                |
| Document       | Individual record                 |
| MongoDB Driver | Official Node.js database library |
| Mongoose       | ODM library                       |
| Schema         | Defines document structure        |
| Model          | Provides database operations      |
| CRUD           | Create, Read, Update, Delete      |
| Query          | Finds documents using conditions  |
| Validation     | Checks data against rules         |

### Quick Revision

```
Node.js
   |
   v
Mongoose / MongoDB Driver
   |
   v
MongoDB
   |
   v
Database
   |
   v
Collection
   |
   v
Documents
```

Chapter 26 Completed

## Next: Chapter 27 — Mongoose

In the next chapter, we will study Mongoose in more detail:

1. Schema
2. Model
3. Documents
4. Validation
5. Default values
6. Required fields
7. Unique fields
8. Timestamps
9. Middleware
10. Populate
11. References

We will also learn how to connect two collections, such as Students and Courses, using Mongoose references and `populate()`.

Type `NEXT` to start Chapter 27 — Mongoose.