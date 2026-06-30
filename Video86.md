# CommonJS vs ECMAScript Modules (ES Modules)

## What are Modules?

* A module is a reusable piece of code that can be imported and used in another file.
* Modules help divide large applications into smaller, manageable parts.

Example:

```
project/
│
├── main.js
├── math.js
└── user.js
```

---

# Types of JavaScript Modules

JavaScript mainly has two module systems:

1. CommonJS (CJS)
2. ECMAScript Modules (ESM)

---

# 1. CommonJS Modules

* CommonJS is the older module system mainly used in Node.js.
* It uses:

```
require()
```

for importing modules.

Example:

```js
const fs = require("fs");
```

Here:

* `fs` is the File System module
* `require()` loads the module

---

## Exporting in CommonJS

Syntax:

```js
module.exports = value;
```

Example:

math.js

```js
const add = (a,b)=>{
    return a+b;
}

module.exports = add;
```

Using it:

main.js

```js
const add = require("./math");

console.log(add(2,3));
```

Output:

```
5
```

---

# 2. ECMAScript Modules (ES Modules)

* ES Modules are the modern JavaScript standard.
* Used in both:

  * Browser JavaScript
  * Modern Node.js

They use:

```
import
export
```

---

## Exporting in ES Modules

math.js

```js
export const add = (a,b)=>{
    return a+b;
}
```

---

## Importing in ES Modules

main.js

```js
import {add} from "./math.js";

console.log(add(2,3));
```

Output:

```
5
```

---

# Enabling ES Modules in Node.js

Add this in `package.json`:

```json
{
  "type": "module"
}
```

Now Node.js treats `.js` files as ES Modules.

---

# Default Export

A module can export one main value.

Example:

```js
export default function hello(){
    console.log("Hello");
}
```

Import:

```js
import hello from "./file.js";
```

---

# CommonJS vs ES Modules

| Feature      | CommonJS       | ES Modules                    |
| ------------ | -------------- | ----------------------------- |
| Import       | require()      | import                        |
| Export       | module.exports | export                        |
| Created for  | Node.js        | JavaScript standard           |
| Loading      | Synchronous    | Supports asynchronous loading |
| Modern usage | Older projects | New projects                  |

---

# Example Comparison

## CommonJS

Export:

```js
module.exports = {
    a:1,
    b:2
}
```

Import:

```js
const data = require("./file");
```

---

## ES Modules

Export:

```js
export const a = 1;
export const b = 2;
```

Import:

```js
import {a,b} from "./file.js";
```

---

# Node.js Important Concepts

## npm

Node Package Manager

Used to install packages:

```bash
npm install package-name
```

---

## npm init

Creates package.json:

```bash
npm init -y
```

`package.json` stores:

* Project information
* Dependencies
* Module type

---

## nodemon

Automatically restarts server when files change.

Install:

```bash
npm install -g nodemon
```

Run:

```bash
nodemon server.js
```

---

# Node Version Manager (NVM)

* Helps manage multiple Node.js versions.
* Useful when different projects require different Node versions.

Example:

```
Project A → Node 18
Project B → Node 20
```

NVM allows switching between them.

---

# Important Node.js Built-in Modules

Examples:

## HTTP Module

Used to create servers:

```js
const http = require("http");
```

## File System Module

Used for file operations:

```js
const fs = require("fs");
```

---

# Why use Modules?

Benefits:

* Code organization
* Reusability
* Easier debugging
* Better project structure
* Team collaboration

---

# One Line Summary

**CommonJS uses require() and module.exports, while ES Modules use import and export and are the modern JavaScript standard.**
