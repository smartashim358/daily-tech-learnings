# 🔐 Secure Auth API – Backend Learning Notes

> **Goal:** Build a clean, professional authentication API using **Node.js, Express, MongoDB, and JWT**.  
> These notes reflect *real backend development practices*, written clearly for learning + portfolio.

---

## 📌 What We Learned Today (High Level)

- How a **real backend project is structured**
- Connecting **MongoDB** with **Mongoose**
- Creating **User model**
- Building **Register & Login APIs**
- Password hashing using **bcrypt**
- Authentication using **JWT (stateless auth)**
- Protecting routes using **middleware**
- How backend APIs are tested using **Postman**

---

## 🗂️ Project Folder Structure (Industry Style)

```
service-auth-api/
│
├── server.js
├── .env
├── package.json
│
└── src/
    ├── app.js
    ├── config/
    │   └── db.js
    ├── models/
    │   └── User.js
    ├── routes/
    │   └── auth.route.js
    ├── controllers/
    │   └── auth.controller.js
    └── middlewares/
        └── auth.middleware.js
```

> This structure keeps code **scalable**, **readable**, and **team-friendly**.

---

## ⚙️ server.js (App Entry Point)

```js
const app = require("./src/app");

const PORT = process.env.PORT || 3030;

app.listen(PORT, () => {
  console.log(`Server running on http://localhost:${PORT}`);
});
```

**Why?**  
- Keeps server startup separate from app logic
- Makes testing and scaling easier

---

## ⚙️ app.js (App Configuration)

```js
const express = require("express");
const connectDB = require("./config/db");

const app = express();

app.use(express.json());
connectDB();

app.use("/api/auth", require("./routes/auth.route"));

module.exports = app;
```

**Why?**  
- All middleware & routes live here
- Clean separation of concerns

---

## 🛢️ MongoDB Connection (config/db.js)

```js
const mongoose = require("mongoose");

const connectDB = async () => {
  try {
    await mongoose.connect(process.env.MONGO_URI);
    console.log("DB connected");
  } catch (error) {
    console.error("DB error:", error.message);
    process.exit(1);
  }
};

module.exports = connectDB;
```

**Key Points:**
- Uses environment variables
- Proper error handling

---

## 👤 User Model (models/User.js)

```js
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema(
  {
    name: { type: String, required: true },
    email: { type: String, required: true, unique: true },
    password: { type: String, required: true }
  },
  { timestamps: true }
);

module.exports = mongoose.model("User", userSchema);
```

**Why Mongoose Model?**  
- Defines data structure
- Handles validation automatically

---

## 🔐 Auth Controller (controllers/auth.controller.js)

### ✅ Register User

```js
const User = require("../models/User");
const bcrypt = require("bcryptjs");
const jwt = require("jsonwebtoken");

exports.register = async (req, res) => {
  try {
    const { name, email, password } = req.body;

    const hashedPassword = await bcrypt.hash(password, 10);

    const user = await User.create({
      name,
      email,
      password: hashedPassword
    });

    res.status(201).json({
      message: "User registered successfully",
      user
    });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
};
```

---

### ✅ Login User + JWT

```js
exports.login = async (req, res) => {
  try {
    const { email, password } = req.body;

    const user = await User.findOne({ email });
    if (!user) return res.status(404).json({ message: "User not found" });

    const isMatch = await bcrypt.compare(password, user.password);
    if (!isMatch) return res.status(401).json({ message: "Invalid credentials" });

    const token = jwt.sign(
      { userId: user._id },
      process.env.JWT_SECRET,
      { expiresIn: "1d" }
    );

    res.json({ message: "Login successful", token });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
};
```

---

## 🛣️ Routes (routes/auth.route.js)

```js
const express = require("express");
const router = express.Router();
const { register, login } = require("../controllers/auth.controller");

router.post("/register", register);
router.post("/login", login);

module.exports = router;
```

**Final API Endpoints:**
- `POST /api/auth/register`
- `POST /api/auth/login`

---

## 🛡️ JWT Middleware (middlewares/auth.middleware.js)

```js
const jwt = require("jsonwebtoken");

module.exports = (req, res, next) => {
  const authHeader = req.headers.authorization;

  if (!authHeader) {
    return res.status(401).json({ message: "No token provided" });
  }

  const token = authHeader.split(" ")[1];

  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    next();
  } catch (error) {
    res.status(401).json({ message: "Invalid token" });
  }
};
```

---

## 🧠 Key Backend Concepts Covered

- Stateless authentication (JWT)
- Password security (hashing)
- Middleware pattern
- Clean API structure
- Real-world backend flow

---

## ✅ Current Status

- Auth API working
- MongoDB connected
- JWT implemented
- Ready for **portfolio-level projects**

---

## 🚀 Next Steps

- Refresh tokens
- Role-based access (admin/user)
- Input validation
- Rate limiting & security
- Deploy to cloud

---



