# Backend from CodeWithHarry

## Introduction to Express.js (Tutorial #88) – Short Revision Notes

---

# What is Express.js?

- Express.js is a **minimal and flexible web framework** for Node.js.
- It simplifies building:
  - Web servers
  - REST APIs
  - Backend applications
- Built on top of Node.js.

Install:
```bash
npm install express
```

Import:

```javascript
const express = require("express");
```

---

# Creating an Express Server

```javascript
const express = require("express");
const app = express();

app.listen(3000, () => {
    console.log("Server started");
});
```

- `express()` creates the application.
- `app.listen()` starts the server.

---

# Routes

Routes define what happens when a user visits a URL.

Example:

```javascript
app.get("/", (req, res) => {
    res.send("Hello World");
});
```

- `/` → Home route
- `req` → Request object
- `res` → Response object

---

# Different HTTP Methods

### GET

Used to retrieve data.

```javascript
app.get("/about", (req, res) => {
    res.send("About Page");
});
```

---

### POST

Used to send data.

```javascript
app.post("/login", (req, res) => {
    res.send("Login Successful");
});
```

---

### Other Methods

- PUT → Update data
- DELETE → Delete data
- PATCH → Partially update data

---

# Sending Responses

### Text

```javascript
res.send("Hello");
```

---

### HTML

```javascript
res.send("<h1>Hello</h1>");
```

---

### JSON

```javascript
res.json({
    name: "Harry",
    age: 25
});
```

---

# Multiple Routes

```javascript
app.get("/", (req, res) => {
    res.send("Home");
});

app.get("/about", (req, res) => {
    res.send("About");
});

app.get("/contact", (req, res) => {
    res.send("Contact");
});
```

---

# Request Object (`req`)

Contains information sent by the client.

Examples:

```javascript
req.params
req.query
req.body
req.headers
```

---

# Response Object (`res`)

Used to send responses back.

Common methods:

```javascript
res.send()
res.json()
res.status()
res.sendFile()
```

Example:

```javascript
res.status(404).send("Page Not Found");
```

---

# Route Parameters

Dynamic values in URLs.

Example:

```javascript
app.get("/user/:id", (req, res) => {
    res.send(req.params.id);
});
```

URL:

```
/user/101
```

Output:

```
101
```

---

# Query Parameters

Sent after `?` in URL.

Example:

```
/search?name=Harry&age=20
```

Access using:

```javascript
req.query
```

Example:

```javascript
console.log(req.query.name);
```

---

# Nodemon

Automatically restarts the server whenever files change.

Install:

```bash
npm install -g nodemon
```

Run:

```bash
nodemon app.js
```

No need to restart the server manually after every change.

---

# Why Use Express?

- Less code than Node.js HTTP module
- Easy routing
- Middleware support
- REST API development
- Large ecosystem
- Fast development

---

# Typical Express Application Flow

```
Client Request
      │
      ▼
Express Server
      │
      ▼
Route Matches
      │
      ▼
Process Request
      │
      ▼
Send Response
```

---

# Basic Server Example

```javascript
const express = require("express");

const app = express();

app.get("/", (req, res) => {
    res.send("Hello Express");
});

app.get("/about", (req, res) => {
    res.send("About Page");
});

app.listen(3000, () => {
    console.log("Server running on port 3000");
});
```

Run:

```bash
node app.js
```

Visit:

```
http://localhost:3000
```

---

# Quick Revision

- Express is a framework built on Node.js.
- Install using `npm install express`.
- `express()` creates the app.
- `app.listen()` starts the server.
- Routes are created using `app.get()`, `app.post()`, etc.
- `req` contains client request data.
- `res` sends the response.
- Use `req.params` for route parameters.
- Use `req.query` for query strings.
- `res.send()` sends text/HTML.
- `res.json()` sends JSON.
- Nodemon automatically restarts the server during development.
```
