# Middlewares in Express.js | Sigma Web Development Course - Tutorial #90
### Brief Revision Notes

---

# What is Middleware?

Middleware is a **function that executes between receiving the client's request and sending the response**.

It has access to:
- Request object (`req`)
- Response object (`res`)
- Next middleware function (`next`)

It can:
- Execute code
- Modify request/response
- End the request-response cycle
- Pass control to the next middleware

**Flow:**

```
Client Request
      ↓
Middleware 1
      ↓
Middleware 2
      ↓
Route Handler
      ↓
Response
```

---

# Syntax of Middleware

```javascript
app.use((req, res, next) => {
    console.log("Middleware executed");
    next();
});
```

### Explanation

- `req` → Incoming request
- `res` → Outgoing response
- `next()` → Passes control to the next middleware

Without `next()`, the request gets stuck.

---

# app.use()

Used to register middleware.

```javascript
app.use(middlewareFunction);
```

Runs for **every request** unless a specific path is provided.

Example:

```javascript
app.use((req,res,next)=>{
    console.log("Hello");
    next();
});
```

---

# Middleware Execution Order

Middlewares execute **from top to bottom**.

Example

```javascript
app.use((req,res,next)=>{
    console.log("First");
    next();
});

app.use((req,res,next)=>{
    console.log("Second");
    next();
});

app.get("/",(req,res)=>{
    res.send("Home");
});
```

Output

```
First
Second
Home
```

---

# Importance of next()

`next()` transfers control to the next middleware or route.

Example

```javascript
app.use((req,res,next)=>{
    console.log("Middleware");
    next();
});
```

If omitted

```javascript
app.use((req,res,next)=>{
    console.log("Middleware");
});
```

Browser keeps loading because Express doesn't know what to do next.

---

# Ending Middleware

A middleware can directly send the response.

Example

```javascript
app.use((req,res,next)=>{
    res.send("Blocked");
});
```

Since response is already sent,
the remaining middlewares and route handlers won't execute.

---

# Multiple Middlewares

```javascript
app.use((req,res,next)=>{
    console.log("1");
    next();
});

app.use((req,res,next)=>{
    console.log("2");
    next();
});

app.use((req,res,next)=>{
    console.log("3");
    next();
});
```

Execution

```
1
2
3
```

---

# Middleware for Specific Route

Instead of every request, middleware can run only on a path.

```javascript
app.use("/about",(req,res,next)=>{
    console.log("About middleware");
    next();
});
```

Runs only for

```
/about
/about/us
/about/team
```

Doesn't run for

```
/
/contact
/login
```

---

# Creating Custom Middleware

Example

```javascript
const logger = (req,res,next)=>{
    console.log(req.method, req.url);
    next();
};

app.use(logger);
```

Output

```
GET /
POST /login
GET /about
```

---

# Logging Middleware

Used to log request details.

```javascript
app.use((req,res,next)=>{
    console.log(`${req.method} ${req.url}`);
    next();
});
```

Example Output

```
GET /
POST /login
DELETE /user
```

---

# Authentication Middleware

Checks whether user is authenticated.

Example

```javascript
app.use((req,res,next)=>{
    let loggedIn = true;

    if(loggedIn){
        next();
    }
    else{
        res.send("Unauthorized");
    }
});
```

---

# Request Time Middleware

```javascript
app.use((req,res,next)=>{
    console.log(new Date());
    next();
});
```

Useful for

- Logging
- Analytics
- Monitoring

---

# Request Object in Middleware

Middleware can access

```javascript
req.method
req.url
req.headers
req.body
req.params
req.query
```

Example

```javascript
app.use((req,res,next)=>{
    console.log(req.method);
    console.log(req.url);
    next();
});
```

---

# Modifying Request Object

Middleware can add custom properties.

```javascript
app.use((req,res,next)=>{
    req.user = "Harry";
    next();
});
```

Route

```javascript
app.get("/",(req,res)=>{
    res.send(req.user);
});
```

Output

```
Harry
```

---

# Built-in Middleware

### 1. express.json()

Parses JSON request body.

```javascript
app.use(express.json());
```

---

### 2. express.urlencoded()

Parses HTML form data.

```javascript
app.use(express.urlencoded({extended:true}));
```

---

### 3. express.static()

Serves static files.

```javascript
app.use(express.static("public"));
```

---

# Third-party Middleware

Installed using npm.

Examples

```
morgan
cors
helmet
cookie-parser
express-session
```

Example

```javascript
const morgan = require("morgan");

app.use(morgan("dev"));
```

---

# Route-Level Middleware

Middleware for a single route.

```javascript
const check = (req,res,next)=>{
    console.log("Checking");
    next();
};

app.get("/about",check,(req,res)=>{
    res.send("About");
});
```

Only `/about` uses this middleware.

---

# Chaining Middlewares

```javascript
app.get("/",
    middleware1,
    middleware2,
    middleware3,
    (req,res)=>{
        res.send("Done");
    }
);
```

Execution Order

```
middleware1
↓
middleware2
↓
middleware3
↓
Route Handler
```

---

# Error Handling Middleware (Introduction)

Special middleware with four parameters.

```javascript
app.use((err,req,res,next)=>{
    console.log(err);
    res.send("Something went wrong");
});
```

Express recognizes it because of the four arguments.

---

# Common Uses of Middleware

- Authentication
- Authorization
- Logging
- Request validation
- Error handling
- Parsing request body
- Serving static files
- Rate limiting
- Security
- Session handling

---

# Request Lifecycle

```
Client
   │
   ▼
Middleware 1
   │
   ▼
Middleware 2
   │
   ▼
Middleware 3
   │
   ▼
Route Handler
   │
   ▼
Response
```

---

# Interview Questions

### What is middleware?

A function that runs between receiving the request and sending the response.

---

### What does `next()` do?

Passes control to the next middleware or route handler.

---

### What happens if `next()` is not called?

The request hangs unless a response is sent.

---

### Difference between `app.use()` and `app.get()`?

| app.use() | app.get() |
|-----------|-----------|
| Registers middleware | Handles GET requests |
| Runs before route handler | Sends response |
| Can run for all HTTP methods | Only GET requests |

---

### Difference between Global and Route Middleware

| Global Middleware | Route Middleware |
|-------------------|------------------|
| Runs for all requests | Runs for selected routes |
| Registered using `app.use()` | Added directly to route |

---

# Important Methods to Remember

```javascript
app.use()
next()
express.json()
express.urlencoded()
express.static()
```

---

# Key Points (Exam Revision)

- Middleware executes before route handlers.
- Middleware receives `req`, `res`, and `next`.
- `next()` moves to the next middleware.
- Middleware order matters.
- `app.use()` registers middleware.
- Middleware can modify `req` and `res`.
- Middleware can end the request by sending a response.
- Built-in middleware includes `express.json()`, `express.urlencoded()`, and `express.static()`.
- Route middleware runs only for selected routes.
- Third-party middleware extends Express functionality.

---

# Quick Revision (30 Seconds)

- Middleware = Function between Request & Response.
- Uses `req`, `res`, `next`.
- Register using `app.use()`.
- `next()` is required to continue.
- Order of middleware matters.
- Can be Global or Route-specific.
- Used for logging, authentication, validation, security, parsing, and error handling.
