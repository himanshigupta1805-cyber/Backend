# EJS Template Engine in Express (Tutorial #92) – Revision Notes

---

# What is EJS?

**EJS (Embedded JavaScript)** is a **template engine** for Express.js that allows us to generate **dynamic HTML pages**.

Instead of sending plain HTML, EJS lets us insert JavaScript code inside HTML.

Extension:
```
.ejs
```

Install using npm:

```bash
npm install ejs
```

---

# Why do we need a Template Engine?

Without EJS:

```javascript
res.send("<h1>Hello Himanshi</h1>");
```

or

```javascript
res.sendFile("index.html");
```

Static HTML cannot change based on user data.

With EJS:

```javascript
res.render("index", {
    name: "Himanshi"
});
```

Output:

```
Hello Himanshi
```

Same page can display different data for different users.

---

# Setting up EJS in Express

### Step 1

Install EJS

```bash
npm install ejs
```

---

### Step 2

Tell Express to use EJS.

```javascript
const express = require("express");
const app = express();

app.set("view engine", "ejs");
```

Now Express knows that the template engine is EJS.

---

# Views Folder

By default Express searches for templates inside a folder named:

```
views/
```

Example:

```
Project

│
├── node_modules
├── public
├── views
│      index.ejs
│      about.ejs
│      contact.ejs
│
├── app.js
└── package.json
```

No need to specify the extension while rendering.

```javascript
res.render("index");
```

Express automatically loads

```
views/index.ejs
```

---

# render()

Instead of

```javascript
res.send()
```

we use

```javascript
res.render()
```

Example:

```javascript
app.get("/", (req, res)=>{
    res.render("index");
});
```

---

# Passing Data to EJS

Second argument of render() is an object.

```javascript
app.get("/", (req, res)=>{

    res.render("index", {
        name: "Himanshi",
        age: 20
    });

});
```

Inside EJS

```html
<h1><%= name %></h1>

<p><%= age %></p>
```

Output

```
Himanshi

20
```

---

# EJS Syntax

## 1. Output Variable

```ejs
<%= variable %>
```

Prints the value.

Example

```ejs
<%= name %>
```

Output

```
Himanshi
```

---

## 2. Execute JavaScript

```ejs
<% %>
```

Does not print anything.

Used for:

- loops
- conditions
- variable declarations

Example

```ejs
<%

let x = 10;

%>
```

Nothing appears on webpage.

---

## 3. Comments

```ejs
<%# This is a comment %>
```

Ignored while rendering.

---

# Dynamic Route Example

```javascript
app.get("/profile", (req,res)=>{

    res.render("profile",{
        username:"Harry",
        age:25
    });

});
```

profile.ejs

```ejs
<h1>Welcome <%= username %></h1>

<p>Age : <%= age %></p>
```

---

# Using if-else

Example

```ejs
<%

if(age>=18){

%>

<h2>Eligible</h2>

<%

}
else{

%>

<h2>Not Eligible</h2>

<%

}

%>
```

Only one block is displayed depending on the condition.

---

# Loops in EJS

Example

```javascript
app.get("/",(req,res)=>{

    const fruits = ["Apple","Banana","Mango"];

    res.render("index",{
        fruits
    });

});
```

EJS

```ejs
<ul>

<%

fruits.forEach(function(item){

%>

<li><%= item %></li>

<%

});

%>

</ul>
```

Output

```
• Apple
• Banana
• Mango
```

---

# Accessing URL Parameters

Example

```javascript
app.get("/:name",(req,res)=>{

    res.render("index",{

        name:req.params.name

    });

});
```

Visiting

```
localhost:3000/Himanshi
```

Output

```
Hello Himanshi
```

---

# Accessing Query Parameters

URL

```
localhost:3000/?name=Harry
```

Server

```javascript
app.get("/",(req,res)=>{

    res.render("index",{

        name:req.query.name

    });

});
```

Output

```
Hello Harry
```

---

# Sending Multiple Variables

```javascript
res.render("index",{

    name:"Harry",

    age:25,

    city:"Delhi"

});
```

EJS

```ejs
<h1><%= name %></h1>

<p><%= age %></p>

<p><%= city %></p>
```

---

# Example Project Structure

```
Project
│
├── node_modules
│
├── public
│      style.css
│
├── views
│      index.ejs
│      profile.ejs
│      about.ejs
│
├── app.js
├── package.json
└── package-lock.json
```

---

# Using CSS with EJS

Serve static files.

```javascript
app.use(express.static("public"));
```

Folder

```
public

    style.css
```

Inside EJS

```html
<link rel="stylesheet" href="/style.css">
```

---

# Flow of Execution

```
Browser
      │
      ▼
Request
      │
      ▼
Express Route
      │
      ▼
res.render()
      │
      ▼
EJS Template
      │
      ▼
Dynamic HTML Generated
      │
      ▼
Browser
```

---

# res.send() vs res.render()

| res.send() | res.render() |
|------------|--------------|
| Sends plain text/HTML | Renders an EJS template |
| Mostly static | Dynamic |
| No template engine | Uses template engine |
| Simple responses | Dynamic webpages |

---

# EJS Advantages

- Easy to learn
- Integrates seamlessly with Express
- Supports JavaScript directly
- Dynamic HTML generation
- Reusable templates
- Supports loops and conditions
- Pass data from backend easily
- Ideal for server-side rendering

---

# Limitations

- Server-side rendering only
- Less interactive than frontend frameworks like React
- Large projects can become harder to maintain without proper organization

---

# Important Interview Questions

### What is EJS?

A template engine used with Express to generate dynamic HTML pages using JavaScript.

---

### Which folder stores EJS templates?

```
views/
```

---

### Which command installs EJS?

```bash
npm install ejs
```

---

### How do we enable EJS?

```javascript
app.set("view engine", "ejs");
```

---

### Which function renders an EJS page?

```javascript
res.render();
```

---

### Difference between send() and render()?

- `send()` → Sends plain text/HTML.
- `render()` → Generates HTML from an EJS template.

---

### How do you print a variable in EJS?

```ejs
<%= variable %>
```

---

### How do you execute JavaScript without printing it?

```ejs
<% %>
```

---

### How do you write comments in EJS?

```ejs
<%# comment %>
```

---

### Can EJS use loops?

Yes.

```ejs
<%

array.forEach(item=>{

%>

<%= item %>

<%

})

%>
```

---

### Can EJS use if-else statements?

Yes.

```ejs
<%

if(condition){

%>

...

<%

}

%>
```

---

# Quick Revision

- Install EJS
  ```bash
  npm install ejs
  ```

- Enable template engine
  ```javascript
  app.set("view engine","ejs");
  ```

- Templates go inside
  ```
  views/
  ```

- Render template
  ```javascript
  res.render("index");
  ```

- Pass data
  ```javascript
  res.render("index",{name:"Harry"});
  ```

- Print variable
  ```ejs
  <%= name %>
  ```

- Execute JavaScript
  ```ejs
  <% %>
  ```

- Comment
  ```ejs
  <%# comment %>
  ```

- Loops and conditions are fully supported.

---

# Key Takeaways

- EJS is Express's most commonly used template engine for server-side rendering.
- `app.set("view engine", "ejs")` configures Express to use EJS.
- All `.ejs` files are placed inside the `views` directory by default.
- `res.render()` is used instead of `res.send()` to render dynamic pages.
- Data is passed from the backend to templates through the second argument of `res.render()`.
- `<%= %>` prints values, while `<% %>` executes JavaScript without displaying output.
- EJS supports variables, loops, conditions, URL parameters, query parameters, and static assets, making it ideal for creating dynamic Express applications.
