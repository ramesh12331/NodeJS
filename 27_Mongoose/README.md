# 📘 PART 7 — DATABASES

# Chapter 27 — Mongoose



Beginner to Intermediate

Practical Learning



In Chapter 26, we learned MongoDB basics, database connections, schemas, models and CRUD operations.

Now we will study Mongoose in detail, with practical examples.

## 📚 Chapter Topics

1. What is Mongoose?
2. Mongoose Architecture
3. Schema
4. Model
5. Documents
6. Schema Data Types
7. Validation
8. Default Values
9. Required Fields
10. Unique Fields
11. Timestamps
12. Middleware (Hooks)
13. References
14. Populate
15. Practical Student and Course Relationship
16. Interview Questions
17. Practice Exercises
18. Chapter Summary

## 1. What is Mongoose?

Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js.

It helps us work with MongoDB using JavaScript objects and provides features such as:

- Schema definition
- Models
- Validation
- Default values
- Middleware
- Relationships using references
- Populate

### Without Mongoose

Using the MongoDB Driver:

```
const { MongoClient } = require("mongodb");

// Create MongoDB client
const client = new MongoClient("mongodb://127.0.0.1:27017");

async function createStudent() {

    await client.connect();

    const db = client.db("collegeDB");

    const students = db.collection("students");

    // Insert student
    await students.insertOne({
        name: "Ramesh",
        age: 25,
        course: "Node.js"
    });

    await client.close();
}

createStudent();
```

### With Mongoose

```
const mongoose = require("mongoose");

// Define schema
const studentSchema = new mongoose.Schema({
    name: String,
    age: Number,
    course: String
});

// Create model
const Student = mongoose.model("Student", studentSchema);

// Create student
async function createStudent() {

    const student = await Student.create({
        name: "Ramesh",
        age: 25,
        course: "Node.js"
    });

    console.log(student);
}
```

Mongoose provides a schema-based way to organize and manage MongoDB data.

## 2. Mongoose Architecture

Understand how Mongoose communicates with MongoDB.

```
        CLIENT / POSTMAN
                |
                v
          EXPRESS SERVER
                |
                v
           CONTROLLER
                |
                v
            MODEL
                |
                v
            SCHEMA
                |
                v
             MONGOOSE
                |
                v
             MONGODB
                |
                v
           COLLECTION
                |
                v
            DOCUMENT
```

### Important terms

| Term       | Meaning                      |
| ---------- | ---------------------------- |
| Schema     | Defines document structure   |
| Model      | Provides database operations |
| Document   | One record in a collection   |
| Mongoose   | ODM library                  |
| Collection | Group of MongoDB documents   |

## 3. What is a Schema?

A Schema defines the structure, fields, data types and validation rules of documents.

Example:

```
const mongoose = require("mongoose");

const studentSchema = new mongoose.Schema({

    name: String,

    age: Number,

    email: String,

    course: String

});
```

### Understanding the schema

```
Student Schema
      |
      |---- name      String
      |
      |---- age       Number
      |
      |---- email     String
      |
      |---- course    String
```

Here:

- `name` is a field.
- `String` is its data type.
- `age` is another field.
- `Number` is its data type.

### Why do we need a schema?

Imagine these three student records:

```
[
    {
        "name": "Ramesh",
        "age": 25
    },
    {
        "name": "Kiran",
        "age": "twenty"
    },
    {
        "name": "Arun",
        "age": 28
    }
]
```

The second student's age is a string instead of a number.

A Mongoose schema helps us define and enforce the expected structure.

## 4. What is a Model?

A Model is created from a Schema and provides methods to interact with a MongoDB collection.

Example:

```
const mongoose = require("mongoose");

// Create schema
const studentSchema = new mongoose.Schema({

    name: String,
    age: Number

});

// Create model
const Student = mongoose.model("Student", studentSchema);
```

Now we can perform database operations.

### Create

```
await Student.create({
    name: "Ramesh",
    age: 25
});
```

### Read

```
const students = await Student.find();
```

### Update

```
await Student.findByIdAndUpdate(
    "STUDENT_ID",
    { age: 26 }
);
```

### Delete

```
await Student.findByIdAndDelete("STUDENT_ID");
```

### Schema vs Model

| Schema             | Model                        |
| ------------------ | ---------------------------- |
| Defines structure  | Interacts with collection    |
| Defines fields     | Provides CRUD methods        |
| Defines validation | Executes database operations |

Memory trick: Schema = Structure. Model = Operations.

## 5. What are Documents?

A document is one individual record stored inside a MongoDB collection.

Example:

```
{
    "_id": "673abc123",
    "name": "Ramesh",
    "age": 25,
    "email": "ramesh@gmail.com"
}
```

This is one student document.

### Create a document using a Model

```
const student = new Student({

    name: "Ramesh",
    age: 25

});

// Save document
await student.save();
```

Another way:

```
const student = await Student.create({

    name: "Kiran",
    age: 23

});
```

Both approaches create and save a document.

### Document methods

| Method        | Purpose                                              |
| ------------- | ---------------------------------------------------- |
| `save()`      | Save document                                        |
| `deleteOne()` | Delete document                                      |
| `updateOne()` | Update document                                      |
| `toObject()`  | Convert document into a plain JavaScript object      |
| `toJSON()`    | Convert document into JSON-compatible representation |

## 6. Mongoose Schema Data Types

Mongoose supports several schema data types.

| Data type | Purpose             | Example                          |
| --------- | ------------------- | -------------------------------- |
| String    | Text                | `"Ramesh"`                       |
| Number    | Numeric value       | `25`                             |
| Boolean   | True or false       | `true`                           |
| Date      | Date and time       | `new Date()`                     |
| Array     | Multiple values     | `["Node", "React"]`              |
| ObjectId  | MongoDB document ID | `mongoose.Schema.Types.ObjectId` |
| Mixed     | Flexible data       | `mongoose.Schema.Types.Mixed`    |
| Map       | Key-value data      | `Map`                            |

### Example

```
const studentSchema = new mongoose.Schema({

    name: {
        type: String
    },

    age: {
        type: Number
    },

    isActive: {
        type: Boolean
    },

    joiningDate: {
        type: Date
    },

    skills: {
        type: [String]
    }

});
```

Example document:

```
{
    "name": "Ramesh",
    "age": 25,
    "isActive": true,
    "joiningDate": "2026-11-06T00:00:00.000Z",
    "skills": ["Node.js", "React", "MongoDB"]
}
```

## 7. Mongoose Validation

Validation checks whether document values follow the rules defined in the schema.

For example:

- Name should be required.
- Age should be positive.
- Email should be valid.
- Course should not be empty.

### Example

```
const studentSchema = new mongoose.Schema({

    name: {
        type: String,
        required: true
    },

    age: {
        type: Number,
        min: 1,
        max: 120
    },

    email: {
        type: String,
        required: true,
        match: /^[^\s@]+@[^\s@]+\.[^\s@]+$/
    },

    course: {
        type: String,
        required: true
    }

});
```

### Try invalid data

```
await Student.create({

    name: "Ramesh",
    age: -10,
    email: "invalid-email",
    course: "Node.js"

});
```

Expected result: Mongoose validation error because age is below the minimum and the email does not match the pattern.

### Important validation options

| Validator   | Purpose                    |
| ----------- | -------------------------- |
| `required`  | Field must be provided     |
| `min`       | Minimum number             |
| `max`       | Maximum number             |
| `minLength` | Minimum string length      |
| `maxLength` | Maximum string length      |
| `enum`      | Only allowed values        |
| `match`     | Match a regular expression |
| `validate`  | Custom validation          |

## 8. Default Values

A default value is automatically assigned when a field is not provided.

Example:

```
const studentSchema = new mongoose.Schema({

    name: {
        type: String,
        required: true
    },

    course: {
        type: String,
        default: "Not Assigned"
    },

    isActive: {
        type: Boolean,
        default: true
    }

});
```

### Create student

```
const student = await Student.create({

    name: "Ramesh"

});
```

Expected document:

```
{
    "name": "Ramesh",
    "course": "Not Assigned",
    "isActive": true
}
```

### Dry run

| Field    | User input   | Stored value |
| -------- | ------------ | ------------ |
| name     | Ramesh       | Ramesh       |
| course   | Not provided | Not Assigned |
| isActive | Not provided | true         |

Remember: Mongoose applies a default when a field is `undefined`. It does not replace every empty or `null` value with the default.

## 9. Required Fields

`required: true` means the field must have a value.

Example:

```
const studentSchema = new mongoose.Schema({

    name: {
        type: String,
        required: true
    },

    email: {
        type: String,
        required: true
    },

    age: {
        type: Number,
        required: true
    }

});
```

### Valid data

```
{
    "name": "Ramesh",
    "email": "ramesh@gmail.com",
    "age": 25
}
```

### Invalid data

```
{
    "name": "Ramesh",
    "age": 25
}
```

The email field is missing.

Mongoose returns a validation error.

### Custom required error message

```
email: {
    type: String,
    required: [true, "Email is required"]
}
```

This provides a meaningful validation message.

## 10. Unique Fields

The `unique: true` option creates a unique index so that duplicate values are not allowed in that indexed field.

Example:

```
const studentSchema = new mongoose.Schema({

    name: {
        type: String,
        required: true
    },

    email: {
        type: String,
        required: true,
        unique: true
    }

});
```

### First student

```
{
    "name": "Ramesh",
    "email": "ramesh@gmail.com"
}
```

Inserted successfully

### Second student

```
{
    "name": "Kiran",
    "email": "ramesh@gmail.com"
}
```

Duplicate key error

Why?

Both students are using the same email address.

Important interview point: `unique: true` is not a normal Mongoose validator. It creates a MongoDB unique index. Duplicate values produce a MongoDB duplicate-key error, which your application should handle.

## 11. Timestamps

Timestamps automatically store when a document was created and last updated.

Use:

```
const studentSchema = new mongoose.Schema({

    name: String,

    age: Number,

    course: String

}, {
    timestamps: true
});
```

Mongoose automatically adds:

```
{
    "name": "Ramesh",
    "age": 25,
    "course": "Node.js",
    "createdAt": "2026-11-06T00:00:00.000Z",
    "updatedAt": "2026-11-06T00:00:00.000Z"
}
```

### Two important fields

| Field       | Meaning                        |
| ----------- | ------------------------------ |
| `createdAt` | When document was created      |
| `updatedAt` | When document was last updated |

### Why do we need timestamps?

Imagine an e-commerce application.

We need to know:

- When was the order created?
- When was the order last updated?
- When was the customer registered?

Timestamps help us track these details.

## 12. Mongoose Middleware

Mongoose middleware allows us to execute code before or after certain database operations.

It is also called a hook.

For example, before saving a student, we want to convert their name to uppercase.

### Types of middleware

1. Document middleware
2. Query middleware
3. Model middleware
4. Aggregate middleware

For beginners, first understand document and query middleware.

### 12.1 Pre Middleware

`pre()` executes before the specified operation.

Example:

```
const studentSchema = new mongoose.Schema({

    name: String,

    email: String

});

// Before saving document
studentSchema.pre("save", function () {

    this.name = this.name.toUpperCase();

});
```

Create student:

```
const student = await Student.create({

    name: "ramesh",
    email: "ramesh@gmail.com"

});
```

Stored name:

```
RAMESH
```

Here `this` refers to the document being saved.

### 12.2 Post Middleware

`post()` executes after the specified operation completes.

Example:

```
studentSchema.post("save", function (doc) {

    console.log("Student saved successfully");

    console.log(doc.name);

});
```

When a student is saved, this middleware runs after the save operation.

### 12.3 Query Middleware

Query middleware runs before or after certain query operations.

Example:

```
studentSchema.pre("find", function () {

    console.log("Getting students from database");

});
```

Whenever the model executes `find()`, this pre-hook runs.

### Middleware comparison

| Middleware | Purpose                  |
| ---------- | ------------------------ |
| `pre()`    | Runs before an operation |
| `post()`   | Runs after an operation  |

Important: Register schema middleware before compiling the schema into a model. Also, query middleware and document middleware have different `this` contexts.

## 13. References in Mongoose

Now let's understand how two collections can be connected.

Imagine a college application.

We have two collections:

1. Students
2. Courses

A student can enroll in a course.

Instead of storing the complete course details inside every student document, we can store the course document's ObjectId as a reference.

### Student collection

```
{
    "_id": "STUDENT_ID_1",
    "name": "Ramesh",
    "age": 25,
    "course": "COURSE_ID_1"
}
```

### Course collection

```
{
    "_id": "COURSE_ID_1",
    "courseName": "Node.js",
    "duration": "3 Months"
}
```

Here, the student's `course` field contains the ID of a document in the courses collection.

### How to define references

Course Schema

```
const mongoose = require("mongoose");

const courseSchema = new mongoose.Schema({

    courseName: {
        type: String,
        required: true
    },

    duration: {
        type: String,
        required: true
    }

});

const Course = mongoose.model("Course", courseSchema);

module.exports = Course;
```

Student Schema

```
const mongoose = require("mongoose");

const studentSchema = new mongoose.Schema({

    name: {
        type: String,
        required: true
    },

    age: Number,

    course: {
        type: mongoose.Schema.Types.ObjectId,
        ref: "Course"
    }

});

const Student = mongoose.model("Student", studentSchema);

module.exports = Student;
```

### Understanding `ObjectId` and `ref`

```
course: {
    type: mongoose.Schema.Types.ObjectId,
    ref: "Course"
}
```

- `ObjectId` stores a MongoDB document ID.
- `ref: "Course"` tells Mongoose which model the reference belongs to.

## 14. Populate in Mongoose

Populate replaces a referenced document ID with the actual referenced document data when querying.

Without populate:

```
const student = await Student.findOne({
    name: "Ramesh"
});
```

Example result:

```
{
    "_id": "STUDENT_ID_1",
    "name": "Ramesh",
    "age": 25,
    "course": "COURSE_ID_1"
}
```

We only see the course ID.

### With populate

```
const student = await Student.findOne({
    name: "Ramesh"
}).populate("course");
```

Example result:

```
{
    "_id": "STUDENT_ID_1",
    "name": "Ramesh",
    "age": 25,
    "course": {
        "_id": "COURSE_ID_1",
        "courseName": "Node.js",
        "duration": "3 Months"
    }
}
```

Now we can see the course details.

### Populate selected fields

We do not always need every field.

```
const student = await Student.findOne({
    name: "Ramesh"
}).populate("course", "courseName duration");
```

This returns only the selected course fields, along with its ID.

### Populate multiple references

Imagine a student has both a course and a teacher reference.

```
const student = await Student.findById(studentId)
    .populate("course")
    .populate("teacher");
```

Mongoose resolves both references when those paths are configured correctly.

## 15. Practical Project — Student and Course Management

Let's connect everything.

### Project structure

```
college-management/
│
├── config/
│   └── db.js
│
├── models/
│   ├── Student.js
│   └── Course.js
│
├── routes/
│   └── collegeRoutes.js
│
├── controllers/
│   └── collegeController.js
│
├── .env
│
└── server.js
```

### Step 1: Course model

`models/Course.js`

```
const mongoose = require("mongoose");

const courseSchema = new mongoose.Schema({

    courseName: {
        type: String,
        required: true,
        trim: true
    },

    duration: {
        type: String,
        required: true
    },

    fees: {
        type: Number,
        required: true,
        min: 0
    }

}, {
    timestamps: true
});

module.exports = mongoose.model("Course", courseSchema);
```

### Step 2: Student model

`models/Student.js`

```
const mongoose = require("mongoose");

const studentSchema = new mongoose.Schema({

    name: {
        type: String,
        required: true,
        trim: true
    },

    email: {
        type: String,
        required: true,
        unique: true,
        lowercase: true
    },

    age: {
        type: Number,
        required: true,
        min: 1
    },

    course: {
        type: mongoose.Schema.Types.ObjectId,
        ref: "Course",
        required: true
    }

}, {
    timestamps: true
});

module.exports = mongoose.model("Student", studentSchema);
```

### Step 3: Database connection

`config/db.js`

```
const mongoose = require("mongoose");

const connectDB = async () => {

    try {

        await mongoose.connect(process.env.MONGO_URI);

        console.log("MongoDB connected");

    } catch (error) {

        console.log("Database connection error:", error.message);

        process.exit(1);

    }

};

module.exports = connectDB;
```

### Step 4: Controller

`controllers/collegeController.js`

```
const Student = require("../models/Student");
const Course = require("../models/Course");

// Create course
const createCourse = async (req, res) => {

    try {

        const course = await Course.create(req.body);

        res.status(201).json({
            message: "Course created successfully",
            data: course
        });

    } catch (error) {

        res.status(400).json({
            message: error.message
        });

    }

};

// Create student
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

// Get students with course details
const getStudents = async (req, res) => {

    try {

        const students = await Student.find()
            .populate("course", "courseName duration fees");

        res.status(200).json({
            data: students
        });

    } catch (error) {

        res.status(500).json({
            message: error.message
        });

    }

};

module.exports = {
    createCourse,
    createStudent,
    getStudents
};
```

### Step 5: Routes

`routes/collegeRoutes.js`

```
const express = require("express");

const router = express.Router();

const {
    createCourse,
    createStudent,
    getStudents
} = require("../controllers/collegeController");

router.post("/courses", createCourse);

router.post("/students", createStudent);

router.get("/students", getStudents);

module.exports = router;
```

### Step 6: Server

`server.js`

```
const express = require("express");

require("dotenv").config();

const connectDB = require("./config/db");

const collegeRoutes = require("./routes/collegeRoutes");

const app = express();

app.use(express.json());

app.use("/api", collegeRoutes);

const startServer = async () => {

    await connectDB();

    app.listen(3000, () => {
        console.log("Server running on port 3000");
    });

};

startServer();
```

### Step 7: `.env`

```
MONGO_URI=mongodb://127.0.0.1:27017/collegeDB
```

### Step 8: Test using Postman

A. Create Course

POST:

```
http://localhost:3000/api/courses
```

Body:

```
{
    "courseName": "Node.js",
    "duration": "3 Months",
    "fees": 15000
}
```

Copy the generated course `_id` from the response.

B. Create Student

POST:

```
http://localhost:3000/api/students
```

Body:

```
{
    "name": "Ramesh",
    "email": "ramesh@gmail.com",
    "age": 25,
    "course": "PASTE_COURSE_ID_HERE"
}
```

C. Get Students

GET:

```
http://localhost:3000/api/students
```

Expected response structure:

```
{
    "data": [
        {
            "_id": "STUDENT_ID",
            "name": "Ramesh",
            "email": "ramesh@gmail.com",
            "age": 25,
            "course": {
                "_id": "COURSE_ID",
                "courseName": "Node.js",
                "duration": "3 Months",
                "fees": 15000
            }
        }
    ]
}
```

Relationship working

The student document stores the course ID. `populate()` retrieves the matching course details.

## 16. Important Mongoose Methods

| Method                      | Purpose                       |
| --------------------------- | ----------------------------- |
| `mongoose.connect()`        | Connect to MongoDB            |
| `mongoose.model()`          | Create a model                |
| `Model.create()`            | Create document               |
| `Model.find()`              | Find multiple documents       |
| `Model.findOne()`           | Find one document             |
| `Model.findById()`          | Find document by ID           |
| `Model.updateOne()`         | Update matching document      |
| `Model.findByIdAndUpdate()` | Find and update by ID         |
| `Model.deleteOne()`         | Delete matching document      |
| `Model.findByIdAndDelete()` | Find and delete by ID         |
| `populate()`                | Retrieve referenced documents |
| `save()`                    | Save a document               |

## 17. Interview Questions

## 18. Practice Exercises

### Beginner Level

- Create a Student schema.
- Add name, age and email fields.
- Add required validation.
- Add default values.
- Add timestamps.
- Create five student documents.

### Intermediate Level

- Create an Employee schema.
- Add unique email.
- Add salary minimum validation.
- Add an enum for employee department.
- Create pre-save middleware to normalize names.

### Advanced Beginner Level

- Create Student and Course models.
- Add a reference from Student to Course.
- Create a student with a course ID.
- Use populate to retrieve course details.
- Return student and course information through an API.

## 19. Chapter Summary

| Concept    | Meaning                            |
| ---------- | ---------------------------------- |
| Mongoose   | ODM library                        |
| Schema     | Defines document structure         |
| Model      | Performs database operations       |
| Document   | Individual record                  |
| Validation | Checks data                        |
| Default    | Automatically assigns a value      |
| Required   | Makes a field mandatory            |
| Unique     | Creates a unique index             |
| Timestamps | Tracks creation and update time    |
| Middleware | Runs code around operations        |
| Reference  | Stores another document's ID       |
| Populate   | Retrieves referenced document data |

### Quick Revision

```
MONGOOSE
   |
   v
SCHEMA
   |
   v
MODEL
   |
   v
DOCUMENT
   |
   v
MONGODB COLLECTION
   |
   v
DATABASE
```

### Important concepts to remember

- Schema: What fields should a document contain?
- Model: How do we interact with the collection?
- Document: What is one stored record?
- Validation: Is the data correct?
- Middleware: What code should run before or after an operation?
- Reference: How can one document point to another?
- Populate: How can we retrieve the referenced document?

Chapter 27 Completed

## Next learning step

You have now completed the two database chapters in your updated syllabus.

A good next part is PART 8 — NODE.JS AUTHENTICATION AND SECURITY, covering:

1. Authentication vs Authorization
2. Password Hashing with bcrypt
3. Registration API
4. Login API
5. JWT Authentication
6. Access Tokens
7. Protected Routes
8. Role-Based Authorization
9. Refresh Tokens
10. Security Best Practices

Type NEXT when you are ready to begin.