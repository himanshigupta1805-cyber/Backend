# Installing MongoDB & MongoDB Compass (Tutorial #94) - Revision Notes

# MongoDB

- **MongoDB** is a **NoSQL (Non-Relational) Database**.
- Stores data in **Documents (JSON-like BSON format)** instead of tables.
- Collections in MongoDB are similar to tables in SQL.
- Documents are similar to rows in SQL.

### SQL vs MongoDB

| SQL | MongoDB |
|------|----------|
| Database | Database |
| Table | Collection |
| Row | Document |
| Column | Field |

---

# Why MongoDB?

- Flexible schema (documents don't need the same structure).
- Easy to scale horizontally.
- Fast for large datasets.
- Stores nested objects naturally.
- Widely used in MERN Stack.

---

# MongoDB Installation

1. Visit the official MongoDB website.
2. Download **MongoDB Community Server**.
3. Choose:
   - Operating System
   - Version
   - MSI Installer (Windows)
4. Run the installer.

During installation:

- Choose **Complete Installation**.
- Keep default settings.
- Install **MongoDB as a Service** (recommended).
- Leave Data Directory as default.

After installation:
- MongoDB server runs automatically as a Windows Service.

---

# MongoDB Compass

MongoDB itself is only the database server.

To visually manage databases, install:

**MongoDB Compass**

Compass is the GUI for MongoDB.

It allows you to:

- View databases
- Create collections
- Insert documents
- Update documents
- Delete documents
- Run queries

---

# Installing MongoDB Compass

Download MongoDB Compass from MongoDB's official website.

Install normally.

After opening:

- Click **New Connection**
- Default connection string:

```
mongodb://localhost:27017
```

Click **Connect**.

If MongoDB service is running, Compass connects successfully.

---

# Localhost Connection

Default MongoDB server runs on:

```
localhost
```

Default Port:

```
27017
```

Connection URL:

```
mongodb://127.0.0.1:27017
```

or

```
mongodb://localhost:27017
```

Both are equivalent.

---

# Creating a Database

MongoDB does **not** require manually creating databases first.

In Compass:

1. Click **Create Database**
2. Enter:
   - Database Name
   - Collection Name
3. Click Create.

Example:

Database:
```
SigmaDatabase
```

Collection:
```
users
```

---

# Collection

A collection is a group of related documents.

Example:

```
students
employees
products
users
orders
```

---

# Document

Each document stores one record.

Example:

```json
{
  "name": "Harry",
  "age": 24,
  "city": "Delhi"
}
```

Documents are stored in **BSON** (Binary JSON).

---

# BSON

BSON stands for:

**Binary JavaScript Object Notation**

Advantages:

- Faster processing
- Supports more data types than JSON
- Optimized for storage

---

# Inserting Documents

Click:

```
Add Data
→ Insert Document
```

Example:

```json
{
  "name": "Rohan",
  "age": 21,
  "course": "B.Tech"
}
```

Click **Insert**.

MongoDB automatically creates an `_id` field.

---

# _id Field

Every MongoDB document has a unique:

```json
_id
```

Example:

```json
"_id": ObjectId(...)
```

Purpose:

- Unique identification
- Primary key of the document
- Automatically generated if not provided

---

# Editing Documents

Select a document.

Click:

```
Edit
```

Modify fields.

Save.

---

# Deleting Documents

Options:

- Delete one document.
- Delete multiple documents using filters.

---

# Refresh

If changes don't appear immediately:

Click

```
Refresh
```

---

# MongoDB Service

MongoDB server must be running before Compass can connect.

If not:

Compass shows connection error.

---

# Folder Structure (Installed)

Typical installation creates:

- MongoDB Server
- Data Directory
- Log files
- MongoDB Service

---

# Important Default Values

| Item | Value |
|------|--------|
| Host | localhost |
| Port | 27017 |
| Protocol | mongodb:// |
| Default URL | mongodb://localhost:27017 |

---

# Workflow

```
Install MongoDB
        ↓
Install Compass
        ↓
Start MongoDB Service
        ↓
Connect to localhost:27017
        ↓
Create Database
        ↓
Create Collection
        ↓
Insert Documents
        ↓
View/Edit/Delete Documents
```

---

# Key Points to Remember

- MongoDB is a NoSQL document database.
- Data is stored as **Documents** inside **Collections**.
- Documents use **BSON** format.
- MongoDB Compass is the graphical interface for MongoDB.
- Default MongoDB port is **27017**.
- Connection URL:
  ```
  mongodb://localhost:27017
  ```
- Every document contains a unique `_id`.
- Databases and collections can be created directly from Compass.
- MongoDB server must be running before Compass can connect.
- Compass simplifies CRUD operations without using the command line.
