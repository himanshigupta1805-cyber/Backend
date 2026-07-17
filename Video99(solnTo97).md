# Exercise 16 - Solution & Shoutouts (Tutorial #99)

## Objective
- Build a web application that generates random employee data.
- Store the generated data in MongoDB using Mongoose.
- Use Express.js as the backend.
- Use EJS for rendering the frontend.
- Trigger database generation through a button click.

---

# Technologies Used

- Node.js
- Express.js
- MongoDB
- Mongoose
- EJS
- Bootstrap

---

# Project Flow

```
Browser
    ↓
Button Click
    ↓
fetch("/generate")
    ↓
Express Route
    ↓
Generate Random Employees
    ↓
Store in MongoDB
    ↓
Send Response
```

---

# MongoDB Connection

```js
await mongoose.connect("mongodb://localhost:27017/company");
```

- Connects to local MongoDB.
- Creates the database automatically if it doesn't exist.

---

# Employee Model

Fields used:

- name
- salary
- language
- city
- isManager

Example:

```js
{
    name: String,
    salary: Number,
    language: String,
    city: String,
    isManager: Boolean
}
```

---

# Random Data Generation

Arrays used:

```js
const names = [];
const languages = [];
const cities = [];
```

Random element function:

```js
function getElement(arr){
    return arr[Math.floor(Math.random()*arr.length)];
}
```

Used for generating random employee details.

---

# Random Salary

```js
Math.floor(Math.random()*400000)
```

Generates salary between:

```
0 - 399999
```

---

# Random Boolean

```js
Math.random()>0.5
```

Returns:

- true
- false

with approximately equal probability.

---

# Deleting Existing Records

```js
await Employee.deleteMany();
```

Deletes every document before inserting new ones.

Useful for generating fresh random data.

---

# Creating Documents

```js
await Employee.create({
    ...
})
```

Inserts one employee document into MongoDB.

---

# Loop for Multiple Employees

```js
for(let i=0;i<10;i++){
    ...
}
```

Creates 10 random employee records.

---

# Express Routes

## Home Route

```js
app.get("/",...)
```

Displays the webpage.

---

## Generate Route

```js
app.get("/generate",...)
```

Responsible for:

- deleting old records
- generating new records
- inserting into MongoDB

---

# Fetch API

Frontend:

```js
fetch("/generate")
```

Sends request to backend.

---

# JSON Response

Recommended:

```js
res.json({
    success:true
});
```

instead of

```js
res.render(...)
```

because fetch expects JSON.

---

# Common Errors

## 1. Unexpected token '<'

Reason:

Backend sends HTML.

Frontend expects JSON.

Fix:

```js
res.json(...)
```

---

## 2. arr.length is not a function

Wrong:

```js
arr.length()
```

Correct:

```js
arr.length
```

---

## 3. getElement returns undefined

Wrong:

```js
function getElement(arr){
    const index=...
}
```

Correct:

```js
function getElement(arr){
    return arr[index];
}
```

---

## 4. Refreshing `/generate`

Problem:

Every refresh sends

```
GET /generate
```

which again deletes and inserts records.

Recommended solution:

Use

```js
POST /generate
```

instead of

```js
GET /generate
```

---

# Bootstrap UI

Simple interface:

- Heading
- Description
- Generate Button
- Success/Error Message

---

# Best Practices

- Keep data generation in a separate route.
- Prefer POST for database modifications.
- Return JSON for API routes.
- Use helper functions for repeated logic.
- Await asynchronous database operations.
- Store repeated values in arrays.
- Keep frontend and backend responsibilities separate.

---

# Important Commands

Initialize project

```bash
npm init -y
```

Install packages

```bash
npm install express mongoose ejs
```

Run project

```bash
node main.js
```

or

```bash
nodemon main.js
```

---

# Key Concepts Revised

- Express Routing
- MongoDB
- Mongoose
- CRUD (Create/Delete)
- Async/Await
- Fetch API
- JSON Responses
- Bootstrap UI
- Random Data Generation
- EJS Rendering

---

# Interview Questions

### Why use Mongoose?

- Simplifies MongoDB interaction.
- Provides schemas and models.

---

### Why use async/await?

- Handles asynchronous operations cleanly.

---

### Why use fetch()?

- Sends HTTP requests from frontend to backend.

---

### Why use POST instead of GET for insertion?

Because inserting data changes server state.

GET should only retrieve data.

---

### Difference between res.render() and res.json()

| res.render() | res.json() |
|--------------|------------|
| Sends HTML | Sends JSON |
| Used with EJS | Used for APIs |

---

# Quick Revision

- Connect MongoDB using Mongoose.
- Define a model.
- Generate random values.
- Delete previous data.
- Insert new documents.
- Trigger generation from frontend.
- Return JSON to fetch().
- Use POST for database updates.
- Display success message on UI.
