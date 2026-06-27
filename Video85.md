# Backend Notes (Code With Harry)

## Node.js, npm, npx

### Node.js

- Node.js is a runtime environment that allows us to run JavaScript outside the browser.
- Command:

```bash
node file.js
```

---

### npm (Node Package Manager)

- npm comes installed with Node.js.
- It is used to install and manage libraries/packages.

Example:

```bash
npm install react
```

---

### npx (Node Package Execute)

- npx is used to execute packages without permanently installing them.
- Mainly used for creating and running tools.

Example:

```bash
npx create-react-app myapp
```

---

### Relation

```
Node.js → Runs JavaScript
npm → Installs and manages packages
npx → Executes packages
```

---

# What is Slugify?

- URLs usually do not contain spaces or special characters.
- Slugify converts a normal string into a URL-friendly format.

Example:

```
"My New Project"
```

Converted to:

```
my-new-project
```

---

# What is Express.js?

- Express.js is a lightweight backend web framework for Node.js.
- It is used to create web servers and APIs easily.
- It handles requests, routes, and responses.

Example:

```javascript
const express = require("express");

const app = express();

app.get("/", (req, res) => {
    res.send("Hello World");
});

app.listen(3000);
```

### Here:

- `app.get()` → Creates a route
- `req` → Request received from client
- `res` → Response sent to client
- `listen()` → Starts the server

---

## Relation

```
Node.js → Runs JavaScript on server
Express.js → Helps build servers and APIs using Node.js
```
