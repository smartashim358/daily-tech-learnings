# Day 19 of learning (MongoDB &MVC)

> These notes explain **MongoDB and Mongoose** from a backend developer’s mindset.
> No unnecessary theory. Only what you must understand to build real APIs.

---

## 1. Why We Need a Database

Until now, our backend could:
- Receive requests
- Process logic
- Send responses

But data was **temporary**.

Problem:
- Server restarts → data lost
- No real users
- No real applications

So we need **persistent storage**.

---

## 2. What is MongoDB (Simple Definition)

**MongoDB** is a:
- NoSQL database
- Stores data in **documents**, not tables
- Uses **JSON-like** format (called BSON)

Example document:

```json
{
  "_id": "auto-generated",
  "name": "Ashim",
  "email": "ashim@gmail.com"
}
```

MongoDB is chosen because:
- Flexible structure
- Easy to scale
- Perfect for JavaScript backend

---

## 3. MongoDB vs SQL (Short & Clear)

| SQL | MongoDB |
|----|--------|
| Tables | Collections |
| Rows | Documents |
| Fixed schema | Flexible schema |

---

## 4. What is Mongoose and Why We Use It

MongoDB itself is **schema-less**.

That’s dangerous in real apps.

So we use **Mongoose**.

### Definition

**Mongoose** is an ODM (Object Data Modeling) library that:
- Adds schema to MongoDB
- Validates data
- Makes queries easier

Think of Mongoose as:
> “A strict gatekeeper between Express and MongoDB”

---

## 5. Installing Required Packages

```bash
npm install mongoose
```

---

## 6. Connecting MongoDB to Express

### 📁 config/db.js

```js
const mongoose = require("mongoose")

const connectDB = async () => {
  try {
    const conn = await mongoose.connect("mongodb://127.0.0.1:27017/userDB")
    console.log(`MongoDB Connected: ${conn.connection.host}`)
  } catch (error) {
    console.error(error.message)
    process.exit(1)
  }
}

module.exports = connectDB
```

---

### index.js

```js
const express = require("express")
const connectDB = require("./config/db")
const errorHandler = require("./middleware/errorMiddleware")

const app = express()
connectDB()

app.use(express.json())

const userRoutes = require("./routes/userRoutes")
app.use("/api/users", userRoutes)

app.use(errorHandler)

app.listen(5000, () => console.log("Server running on port 5000"))
```

---

## 7. What is a Schema (Very Important)

### Definition

A **schema** defines:
- Fields
- Data types
- Validation rules

This prevents bad data from entering database.

---

## 8. Creating a User Schema

### 📁 models/User.js

```js
const mongoose = require("mongoose")

const userSchema = new mongoose.Schema(
  {
    name: {
      type: String,
      required: true,
      trim: true
    },
    email: {
      type: String,
      required: true,
      unique: true,
      lowercase: true
    }
  },
  {
    timestamps: true
  }
)

module.exports = mongoose.model("User", userSchema)
```

---

## 9. Model (What It Really Is)

### Definition

A **model** is a JavaScript representation of a MongoDB collection.

It lets us:
- Create documents
- Read documents
- Update documents
- Delete documents

---

## 10. Using Model Inside Controller

### controllers/userController.js

```js
const User = require("../models/User")

const getUsers = async (req, res) => {
  const users = await User.find()

  res.status(200).json({
    success: true,
    data: users
  })
}

const createUser = async (req, res) => {
  const { name, email } = req.body

  if (!name || !email) {
    res.status(400)
    throw new Error("Name and email required")
  }

  const userExists = await User.findOne({ email })

  if (userExists) {
    res.status(400)
    throw new Error("User already exists")
  }

  const user = await User.create({ name, email })

  res.status(201).json({
    success: true,
    data: user
  })
}

module.exports = {
  getUsers,
  createUser
}
```

---

## 11. Async Flow (Understand This)

```txt
Request
 ↓
Controller
 ↓
Mongoose Model
 ↓
MongoDB
 ↓
Response
```

Each DB call returns a **Promise** → handled with `await`.

---

## 12. Testing with Postman

### GET
```
GET http://localhost:5000/api/users
```

### POST
```
POST http://localhost:5000/api/users
```

Body:
```json
{
  "name": "Ashim",
  "email": "ashim@gmail.com"
}
```

---

## 13. Common MongoDB Errors

- MongoDB not running
- Wrong connection string
- Duplicate key error (email)
- Forgetting `await`

---

## 14. Why MongoDB Comes After MVC

- MVC gives structure
- MongoDB plugs into controllers cleanly
- Code stays readable
- Scaling becomes easy

---

## 15. What You Can Build Now

- Real REST APIs
- User management systems
- Backend for React apps
- Auth-ready backend

---

## 16. Next Logical Step

- Update & Delete users
- JWT Authentication
- Password hashing
- Role-based access

---

>

