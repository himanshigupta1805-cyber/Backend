# Installing Mongoose & Using it with Express
### Sigma Web Development Course - Tutorial #96 (CodeWithHarry)

---

# What is Mongoose?

- **Mongoose** is an **ODM (Object Data Modeling)** library for MongoDB and Node.js.
- It provides an easier way to interact with MongoDB using JavaScript objects.
- Works on top of the MongoDB Node.js Driver.

### Without Mongoose
```
Express → MongoDB Driver → MongoDB
```

### With Mongoose
```
Express → Mongoose → MongoDB
```

---

# Why Use Mongoose?

- Provides a structured way to work with MongoDB.
- Supports:
  - Schemas
  - Models
  - Validation
  - Default values
  - Middleware (Hooks)
  - Query helpers
  - Cleaner code

---

# Installing Mongoose

Inside your project:

```bash
npm install mongoose
```

Verify installation:

```bash
npm list mongoose
```

---

# Importing Mongoose

CommonJS

```javascript
const mongoose = require("mongoose");
```

ES Modules

```javascript
import mongoose from "mongoose";
```

---

# Connecting to MongoDB

Basic connection:

```javascript
const mongoose = require("mongoose");

mongoose.connect("mongodb://127.0.0.1:27017/company");
```

- `127.0.0.1` → Local MongoDB server
- `27017` → Default MongoDB port
- `company` → Database name

If the database doesn't exist, MongoDB creates it automatically.

---

# Using Async/Await

Recommended way:

```javascript
const mongoose = require("mongoose");

async function main() {
    await mongoose.connect("mongodb://127.0.0.1:27017/company");
}

main();
```

---

# Handling Connection Errors

```javascript
main()
.then(() => {
    console.log("Connected");
})
.catch(err => {
    console.log(err);
});
```

---

# What is a Schema?

A **Schema** defines:

- Fields
- Data types
- Structure of documents
- Validation rules

Example:

```javascript
const employeeSchema = new mongoose.Schema({
    name: String,
    salary: Number,
    language: String,
    city: String,
    isManager: Boolean
});
```

Think of it like a blueprint for documents.

---

# Data Types Supported

Common Mongoose data types:

- String
- Number
- Boolean
- Date
- Array
- Object
- Buffer
- Mixed
- ObjectId

Example:

```javascript
const userSchema = new mongoose.Schema({
    name: String,
    age: Number,
    active: Boolean,
    joined: Date
});
```

---

# Creating a Model

After creating a schema:

```javascript
const Employee = mongoose.model("Employee", employeeSchema);
```

- First argument → Collection name (singular)
- Mongoose automatically converts it into plural.

Example:

```
Employee
↓

employees
```

Collection created automatically.

---

# Creating a Document

Method 1:

```javascript
const employee = new Employee({
    name: "Harry",
    salary: 45000,
    language: "JavaScript",
    city: "Delhi",
    isManager: true
});
```

---

# Saving a Document

```javascript
await employee.save();
```

Complete example:

```javascript
const employee = new Employee({
    name: "Harry",
    salary: 45000,
    language: "JavaScript",
    city: "Delhi",
    isManager: true
});

await employee.save();
```

---

# Creating Document in One Step

Instead of:

```javascript
const employee = new Employee({...});
await employee.save();
```

Use:

```javascript
await Employee.create({
    name: "Harry",
    salary: 45000,
    language: "JavaScript",
    city: "Delhi",
    isManager: true
});
```

---

# Finding Documents

Retrieve all documents:

```javascript
const data = await Employee.find();
```

Find documents matching a condition:

```javascript
const data = await Employee.find({
    city: "Delhi"
});
```

---

# Finding a Single Document

```javascript
const employee = await Employee.findOne({
    city: "Delhi"
});
```

Returns the first matching document.

---

# Updating Documents

Update one:

```javascript
await Employee.updateOne(
    { name: "Harry" },
    { salary: 60000 }
);
```

Update many:

```javascript
await Employee.updateMany(
    { city: "Delhi" },
    { isManager: true }
);
```

---

# Deleting Documents

Delete one:

```javascript
await Employee.deleteOne({
    name: "Harry"
});
```

Delete many:

```javascript
await Employee.deleteMany({
    city: "Delhi"
});
```

---

# Running the Server

Typical Express app:

```javascript
const express = require("express");
const mongoose = require("mongoose");

const app = express();
const port = 3000;
```

Connect MongoDB first:

```javascript
async function main() {
    await mongoose.connect("mongodb://127.0.0.1:27017/company");
}

main();
```

Start server:

```javascript
app.listen(port, () => {
    console.log(`Server running on ${port}`);
});
```

---

# Using Mongoose Inside Routes

Example:

```javascript
app.get("/", async (req, res) => {

    await Employee.create({
        name: "Harry",
        salary: 45000,
        language: "JavaScript",
        city: "Delhi",
        isManager: true
    });

    res.send("Employee Added");
});
```

Whenever `/` is visited:

- Employee is created
- Stored in MongoDB
- Response sent

---

# Viewing Data

Open **MongoDB Compass**

Refresh collection:

```
company
    ↓
employees
```

New document appears.

---

# Flow of Data

```
Browser
    ↓
Express Route
    ↓
Mongoose Model
    ↓
MongoDB Database
```

---

---

# ⭐ Important: Flow of Data

Understanding this flow is crucial for working with Express and Mongoose.

```
Client (Browser/Postman)
          │
          ▼
    Express Route
          │
          ▼
   Mongoose Model
          │
          ▼
     MongoDB Database
          │
          ▼
   Mongoose Model
          │
          ▼
    Express Route
          │
          ▼
Client (Response)
```

### Explanation

1. **Client** sends an HTTP request (GET, POST, PUT, DELETE).
2. **Express Route** receives the request and executes the route handler.
3. The route uses a **Mongoose Model** to perform database operations.
4. **Mongoose** communicates with the **MongoDB database**.
5. MongoDB returns the requested data or confirms the operation.
6. Mongoose passes the result back to the Express route.
7. Express sends the final response back to the client.

### Example

```javascript
app.get("/", async (req, res) => {
    const employees = await Employee.find();
    res.send(employees);
});
```

**Flow for this example:**

```
Browser
   │
GET /
   │
   ▼
Express Route
   │
Employee.find()
   │
   ▼
MongoDB
   │
Returns Employees
   │
   ▼
Express
   │
res.send(employees)
   │
   ▼
Browser
```

> **Remember:** Express never communicates directly with MongoDB. All database operations go through **Mongoose**, which acts as the bridge between your Express application and the MongoDB database.

---

### Model

Represents a MongoDB collection.

```javascript
const Employee = mongoose.model("Employee", employeeSchema);
```

---

### Document

An individual record.

```javascript
{
    name: "Harry",
    salary: 50000
}
```

---

### Collection

Group of documents.

```
employees
```

---

### Database

Contains collections.

```
company
```

---

# Mongoose Workflow

```
Install Mongoose
        ↓
Import Mongoose
        ↓
Connect to MongoDB
        ↓
Create Schema
        ↓
Create Model
        ↓
Create Document
        ↓
Save Document
        ↓
Read / Update / Delete
```

---

# Mongoose vs MongoDB Driver

| MongoDB Driver | Mongoose |
|---------------|----------|
| Low-level API | High-level API |
| No schema | Uses schema |
| More manual work | Cleaner syntax |
| Minimal validation | Built-in validation |
| Flexible | Structured |

---

# Common Methods

| Method | Purpose |
|---------|---------|
| `mongoose.connect()` | Connect database |
| `new mongoose.Schema()` | Create schema |
| `mongoose.model()` | Create model |
| `new Model()` | Create document object |
| `.save()` | Save document |
| `Model.create()` | Create & save document |
| `Model.find()` | Find all documents |
| `Model.findOne()` | Find first matching document |
| `Model.updateOne()` | Update one document |
| `Model.updateMany()` | Update multiple documents |
| `Model.deleteOne()` | Delete one document |
| `Model.deleteMany()` | Delete multiple documents |

---

# Quick Revision

- Mongoose is an ODM for MongoDB.
- Install using `npm install mongoose`.
- Connect using `mongoose.connect()`.
- A **Schema** defines the structure of documents.
- A **Model** maps to a MongoDB collection.
- A **Document** is one record in a collection.
- Use `new Model()` + `.save()` or `Model.create()` to insert data.
- Retrieve data with `find()` or `findOne()`.
- Modify data using `updateOne()` / `updateMany()`.
- Remove data using `deleteOne()` / `deleteMany()`.
- Mongoose automatically creates the database and collection when needed.
- Mongoose makes MongoDB operations cleaner, structured, and easier to manage compared to the native MongoDB driver.
