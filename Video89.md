# Backend from CodeWithHarry
## Response, Request & Routers in Express (Tutorial #89) — Brief Revision Notes

---

# 1. Request (`req`) Object

The `req` object contains all the information sent by the client to the server.

Commonly used properties:

```js
app.get("/", (req, res) => {
    console.log(req);
});
```

### Important Properties

| Property | Description |
|----------|-------------|
| `req.url` | Requested URL |
| `req.method` | HTTP Method (GET, POST, etc.) |
| `req.headers` | Request headers |
| `req.params` | Route parameters |
| `req.query` | Query string parameters |
| `req.body` | Data sent in request body (requires middleware) |

---

## Route Parameters

Dynamic values inside URL.

Example:

```js
app.get("/blog/:slug", (req, res) => {
    console.log(req.params);
});
```

Request:

```
/blog/javascript
```

Output:

```js
{
   slug: "javascript"
}
```

Multiple parameters:

```js
app.get("/user/:id/post/:postId", (req, res) => {
    console.log(req.params);
});
```

Request:

```
/user/25/post/10
```

Output:

```js
{
   id: "25",
   postId: "10"
}
```

---

## Query Parameters

Data sent after `?` in URL.

Example:

```
/search?name=harry&age=25
```

Access using:

```js
req.query
```

Output:

```js
{
   name: "harry",
   age: "25"
}
```

Useful for:

- Searching
- Filtering
- Pagination
- Sorting

---

# 2. Response (`res`) Object

Used to send response back to client.

Example:

```js
app.get("/", (req, res) => {
    res.send("Hello World");
});
```

---

## Common Response Methods

### res.send()

Sends text, HTML or JSON.

```js
res.send("Hello");
```

```js
res.send({
    success: true
});
```

---

### res.json()

Sends JSON response.

```js
res.json({
    name: "Harry",
    age: 25
});
```

---

### res.status()

Sets HTTP status code.

```js
res.status(404).send("Page Not Found");
```

Common Status Codes:

| Code | Meaning |
|------|----------|
| 200 | OK |
| 201 | Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |

---

### res.sendFile()

Sends a file.

```js
res.sendFile("index.html");
```

Usually requires absolute path.

---

### res.redirect()

Redirects to another URL.

```js
res.redirect("/home");
```

---

### res.render()

Used with template engines (EJS, Pug, etc.)

```js
res.render("index");
```

---

# 3. Express Router

Router helps organize routes into separate files.

Instead of writing everything inside one file:

```
app.js
```

Create:

```
routes/
    blog.js
    user.js
    admin.js
```

This keeps projects clean and modular.

---

## Creating a Router

```js
import express from "express";

const router = express.Router();
```

---

## Adding Routes

```js
router.get("/", (req, res) => {
    res.send("Blog Home");
});

router.get("/about", (req, res) => {
    res.send("About Blog");
});
```

---

## Export Router

```js
export default router;
```

---

## Import Router

```js
import blogRouter from "./routes/blog.js";
```

---

## Use Router

```js
app.use("/blog", blogRouter);
```

Now:

```
/blog/
/blog/about
```

are handled inside

```
blog.js
```

---

# Folder Structure

```
Project
│
├── app.js
├── package.json
│
└── routes
      ├── blog.js
      ├── user.js
      └── admin.js
```

---

# app.use()

Mounts middleware or routers.

Example:

```js
app.use("/blog", blogRouter);
```

Meaning:

Every request beginning with

```
/blog
```

goes to

```
blogRouter
```

---

# Request Flow

```
Browser
   │
   ▼
Incoming Request
   │
   ▼
Express App
   │
   ▼
Router
   │
   ▼
Matching Route
   │
   ▼
Controller Function
   │
   ▼
Response (res.send / res.json / etc.)
   │
   ▼
Browser
```

---

# Why Routers?

Without routers:

- Huge `app.js`
- Difficult maintenance
- Hard to debug

With routers:

- Cleaner code
- Better organization
- Easier maintenance
- Modular architecture
- Scalable for large applications

---

# Quick Revision

### Request (`req`)

- Contains client request data
- `req.params`
- `req.query`
- `req.headers`
- `req.body`
- `req.method`
- `req.url`

---

### Response (`res`)

Common methods:

```js
res.send()

res.json()

res.status()

res.sendFile()

res.redirect()

res.render()
```

---

### Router

Create:

```js
const router = express.Router();
```

Add routes:

```js
router.get(...)
router.post(...)
```

Export:

```js
export default router;
```

Use:

```js
app.use("/blog", blogRouter);
```

---

# Exam / Interview Points ⭐

- `req` stores incoming request information.
- `res` sends data back to the client.
- Route Parameters → `req.params`
- Query Parameters → `req.query`
- `express.Router()` creates modular route handlers.
- `app.use()` mounts middleware or routers.
- Routers improve project structure and scalability.
