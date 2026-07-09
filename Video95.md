# CRUD Operations in MongoDB (Tutorial #95) - Revision Notes

# CRUD

CRUD stands for:

- **C** → Create
- **R** → Read
- **U** → Update
- **D** → Delete

These are the four basic operations performed on a database.

---

# MongoDB Shell

CRUD operations can be performed using:

- MongoDB Shell (`mongosh`)
- MongoDB Compass
- Programming languages (Node.js, Python, etc.)

In this tutorial, CRUD operations are demonstrated using **MongoDB Shell**.

---

# Starting MongoDB Shell

Open Command Prompt/Terminal and run:

```bash
mongosh
```

If connected successfully, you'll enter the MongoDB interactive shell.

---

# Viewing Databases

```javascript
show dbs
```

Displays all existing databases.

---

# Selecting a Database

```javascript
use SigmaDatabase
```

- Switches to an existing database.
- If it doesn't exist, MongoDB creates it when data is inserted.

---

# Viewing Current Database

```javascript
db
```

Displays the currently selected database.

---

# Viewing Collections

```javascript
show collections
```

Lists all collections in the current database.

---

# CREATE Operations

## Insert One Document

```javascript
db.users.insertOne({
    name: "Harry",
    age: 24,
    city: "Delhi"
})
```

- Inserts a single document.
- Automatically creates an `_id` field.

---

## Insert Multiple Documents

```javascript
db.users.insertMany([
    {
        name: "Rohan",
        age: 22
    },
    {
        name: "Mohan",
        age: 25
    }
])
```

Inserts multiple documents at once.

---

# READ Operations

## View All Documents

```javascript
db.users.find()
```

Returns every document in the collection.

---

## Pretty Output

```javascript
db.users.find().pretty()
```

Displays documents in a more readable format.

> **Note:** In newer versions of `mongosh`, output is already formatted, so `.pretty()` may not be necessary.

---

## Find One Document

```javascript
db.users.findOne()
```

Returns the first matching document.

---

## Find with Condition

```javascript
db.users.find({
    age: 24
})
```

Returns all documents matching the condition.

---

## Find Multiple Conditions

```javascript
db.users.find({
    city: "Delhi",
    age: 24
})
```

Uses **AND** logic by default.

---

# UPDATE Operations

## Update One Document

```javascript
db.users.updateOne(
    { name: "Harry" },
    {
        $set: {
            age: 25
        }
    }
)
```

Updates the first matching document.

---

## Update Many Documents

```javascript
db.users.updateMany(
    { city: "Delhi" },
    {
        $set: {
            country: "India"
        }
    }
)
```

Updates all matching documents.

---

# `$set` Operator

Used to:

- Add a new field
- Modify an existing field

Example:

```javascript
{
    $set: {
        age: 30
    }
}
```

---

# DELETE Operations

## Delete One Document

```javascript
db.users.deleteOne({
    name: "Harry"
})
```

Deletes the first matching document.

---

## Delete Multiple Documents

```javascript
db.users.deleteMany({
    city: "Delhi"
})
```

Deletes all matching documents.

---

## Delete All Documents

```javascript
db.users.deleteMany({})
```

Deletes every document in the collection.

---

# Query Filters

MongoDB uses JSON-like objects as filters.

Example:

```javascript
{
    age: 24
}
```

Only matching documents are affected.

---

# MongoDB Operators

## Comparison Operators

| Operator | Meaning |
|----------|---------|
| `$gt` | Greater than |
| `$lt` | Less than |
| `$gte` | Greater than or equal to |
| `$lte` | Less than or equal to |
| `$eq` | Equal |
| `$ne` | Not equal |

Example:

```javascript
db.users.find({
    age: { $gt: 20 }
})
```

---

## Logical Operators

### `$and`

```javascript
db.users.find({
    $and: [
        { age: 24 },
        { city: "Delhi" }
    ]
})
```

### `$or`

```javascript
db.users.find({
    $or: [
        { city: "Delhi" },
        { city: "Mumbai" }
    ]
})
```

---

# MongoDB Document Example

```json
{
    "_id": ObjectId("..."),
    "name": "Harry",
    "age": 24,
    "city": "Delhi"
}
```

---

# Common CRUD Workflow

```text
Choose Database
        ↓
Choose Collection
        ↓
Insert Data
        ↓
Read Data
        ↓
Update Data
        ↓
Delete Data
```

---

# Frequently Used Commands

| Command | Purpose |
|----------|---------|
| `show dbs` | List databases |
| `use dbName` | Select database |
| `db` | Show current database |
| `show collections` | List collections |
| `db.collection.find()` | View documents |
| `db.collection.findOne()` | View first matching document |
| `db.collection.insertOne()` | Insert one document |
| `db.collection.insertMany()` | Insert multiple documents |
| `db.collection.updateOne()` | Update one document |
| `db.collection.updateMany()` | Update multiple documents |
| `db.collection.deleteOne()` | Delete one document |
| `db.collection.deleteMany()` | Delete multiple documents |

---

# Key Points to Remember

- CRUD = **Create, Read, Update, Delete**.
- Use `mongosh` to interact with MongoDB through the command line.
- `insertOne()` inserts a single document.
- `insertMany()` inserts multiple documents.
- `find()` retrieves all matching documents.
- `findOne()` returns the first matching document.
- `updateOne()` modifies the first matching document.
- `updateMany()` modifies all matching documents.
- `$set` is used to add or update fields.
- `deleteOne()` removes one document.
- `deleteMany()` removes multiple or all documents.
- Query filters use JSON-like syntax.
- Comparison operators (`$gt`, `$lt`, `$gte`, `$lte`, `$eq`, `$ne`) help filter data.
- Logical operators (`$and`, `$or`) allow combining multiple conditions.
