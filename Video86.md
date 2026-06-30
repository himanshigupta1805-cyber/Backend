
# Backend Modules - Short Notes

## What are Modules?

* Modules are **separate building blocks of a backend application**.
* They divide a large backend into smaller parts, where each module handles a specific functionality.
* Example:

  * User Module → login, signup, profile
  * Product Module → products, search
  * Payment Module → transactions

---

## Why use Modules?

### 1. Clean Code

* Avoids putting the entire backend code in one file.
* Makes the project easier to understand and maintain.

### 2. Easy Debugging

* Problems can be isolated.
* Example: Login issue → check Auth module only.

### 3. Reusability

* A module can be used in multiple places.
* Example: Email module can be used for signup emails and password reset emails.

### 4. Team Collaboration

* Different developers can work on different modules independently.

---

# Types of Modules

## 1. Built-in Modules

* Already provided by the runtime.
* Example in Node.js:

```js
const http = require("http");
```

---

## 2. Custom Modules

* Modules created by developers themselves.

Example:

```
user/
 ├── user.controller.js
 ├── user.routes.js
 └── user.service.js
```

---

## 3. External Modules (Packages)

* Modules created by other developers.
* Installed using package managers like npm.

Example:

```bash
npm install express
```

---

# Why are Modules Installed?

Installed modules provide ready-made functionality.

Instead of writing everything from scratch, we use existing packages.

Example:

## Express.js

Install:

```bash
npm install express
```

Provides:

* Routing
* Middleware
* Request handling

---

## Mongoose

Install:

```bash
npm install mongoose
```

Provides:

* MongoDB connection
* Schema creation
* Database queries

---

## bcrypt

Install:

```bash
npm install bcrypt
```

Used for:

* Password hashing
* Security

---

## jsonwebtoken (JWT)

Install:

```bash
npm install jsonwebtoken
```

Used for:

* User authentication
* Creating login tokens

---

# node_modules Folder

After installing packages:

```
backend/

├── node_modules/
│   ├── express/
│   ├── mongoose/
│   └── bcrypt/
│
├── package.json
└── server.js
```

* `node_modules` contains installed package code.

---

# Simple Flow

```
Developer creates package
          ↓
Package is published
          ↓
We install it using npm
          ↓
We use its features in our backend
```

---

## One Line Summary

**Modules are reusable pieces of code that divide backend functionality and installed modules provide ready-made features to build applications faster.**
