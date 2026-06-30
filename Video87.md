# Working with Files: fs and path Modules (Node.js)

## File System (fs) Module

* `fs` stands for **File System**.
* It is a built-in Node.js module used to work with files.
* It allows us to:

  * Create files
  * Read files
  * Update files
  * Delete files
  * Rename files

Import:

```js
const fs = require("fs");
```

---

# Reading Files

## readFile()

Used to read file contents.

Syntax:

```js
fs.readFile("filename", callback)
```

Example:

```js
const fs = require("fs");

fs.readFile("file.txt", (err, data)=>{
    if(err) throw err;

    console.log(data.toString());
});
```

* `err` → stores errors
* `data` → contains file content

---

# Writing Files

## writeFile()

Used to create a new file or overwrite existing content.

Example:

```js
fs.writeFile("file.txt", "Hello World", ()=>{
    console.log("File written");
});
```

---

# Appending Data

## appendFile()

Adds new content without deleting old content.

Example:

```js
fs.appendFile("file.txt", " New Data", ()=>{
    console.log("Updated");
});
```

---

# Deleting Files

## unlink()

Deletes a file.

Example:

```js
fs.unlink("file.txt", ()=>{
    console.log("Deleted");
});
```

---

# Renaming Files

## rename()

Changes file name.

Example:

```js
fs.rename("old.txt", "new.txt", ()=>{
    console.log("Renamed");
});
```

---

# Synchronous vs Asynchronous Methods

## Asynchronous

* Does not block execution.
* Uses callbacks.

Example:

```js
fs.readFile()
```

Node.js continues other tasks while file operation happens.

---

## Synchronous

* Blocks execution until task completes.

Example:

```js
fs.readFileSync("file.txt");
```

Used when immediate result is required.

---

# Path Module

* `path` is a built-in Node.js module.
* Used to work with file and folder paths.
* Helps create paths that work on different operating systems.

Import:

```js
const path = require("path");
```

---

# path.join()

Combines multiple path segments.

Example:

```js
const fullPath = path.join("folder","file.txt");

console.log(fullPath);
```

Output:

```
folder/file.txt
```

---

# path.extname()

Returns file extension.

Example:

```js
path.extname("app.js")
```

Output:

```
.js
```

---

# path.basename()

Returns file name.

Example:

```js
path.basename("/folder/app.js")
```

Output:

```
app.js
```

---

# path.dirname()

Returns folder path.

Example:

```js
path.dirname("/folder/app.js")
```

Output:

```
/folder
```

---

# __dirname

* Gives current directory path.
* Useful for creating absolute paths.

Example:

```js
console.log(__dirname);
```

---

# Example: Using fs + path Together

```js
const fs = require("fs");
const path = require("path");

const filePath = path.join(__dirname,"data.txt");

fs.writeFile(filePath,"Hello",()=>{
    console.log("File created");
});
```

Flow:

```
path → creates correct file location
fs   → performs file operation
```

---

# Why use fs and path?

## fs Module:

* Manage files
* Store/read data
* Automate file operations

## path Module:

* Handle file locations
* Avoid path errors
* Make code cross-platform

---

# One Line Summary

**fs module is used to perform file operations, while path module is used to handle file and directory paths in Node.js.**
