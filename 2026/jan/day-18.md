# 🧠 What I Learned Today — Express.js Routing (Real‑World Developer Notes) & Day 18

> These notes are written from a **real-world backend developer learning perspective**,  
> not textbook definitions. Everything here reflects **what I actually learned today**,  
> why it exists, how it is used in real projects, and what problems it solves.

---

## 📌 Today’s Focus
Today I learned **Express Router** and understood **why professional backend developers never write all routes in one file**.

Along the way, I also reinforced:
- How requests flow in Express
- How middleware + router work together
- Why project structure matters in real applications

---

## 1️⃣ The Problem We Faced First (Real Situation)
At the beginning, everything was written inside **`server.js` / `index.js`**.

```js
app.get("/users", ...)
app.post("/users", ...)
app.get("/products", ...)
app.post("/products", ...)
```

This works **only for very small apps**.

### Why This Is a Problem in Real Projects
- File becomes very long and unreadable
- Hard to debug errors
- Impossible to scale
- Team collaboration becomes messy

👉 This is where **Express Router** becomes necessary.

---

## 2️⃣ What is Express Router (In Real Terms)
Express Router is a **mini Express app** that handles routes **for one feature only**.

It allows us to:
- Separate logic by feature (users, auth, products)
- Keep main file clean
- Follow industry‑standard backend structure

📌 **Important understanding**  
Router is not optional in real-world backend development — it is a **best practice**.

---

## 3️⃣ Creating a Router File (What We Actually Did)

### 📁 Folder Structure We Learned
```
project/
 ├── routes/
 │    └── userRoutes.js
 ├── server.js
 └── package.json
```

This structure itself is a **real developer habit**.

---

### 🧩 `routes/userRoutes.js`
```js
const express = require("express");
const router = express.Router();

router.get("/", (req, res) => {
  res.send("All users");
});

router.post("/", (req, res) => {
  res.send("Create new user");
});

module.exports = router;
```

### Deep Understanding
- `express.Router()` creates a **separate routing system**
- This file does **not start a server**
- It only defines **user-related endpoints**
- `module.exports` is required, otherwise Express cannot use it

---

## 4️⃣ Connecting Router to Main Server (Critical Step)

### 🧩 `server.js`
```js
const express = require("express");
const app = express();

app.use(express.json());

const userRoutes = require("./routes/userRoutes");
app.use("/users", userRoutes);

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

### What Actually Happens Here
- `/users` becomes the **base route**
- Router decides what happens **after `/users`**
- Express forwards the request internally

---

## 5️⃣ Understanding Request Flow (Very Important)

### Example
```
GET /users
```

### Internal Flow
```
Client
 → Express app
 → app.use("/users")
 → userRoutes router
 → router.get("/")
 → response sent
```

📌 This mental model is **mandatory** for debugging.

---

## 6️⃣ Using req & res Inside Router
Router works **exactly like app**, but in a smaller scope.

### `req.params`
```js
router.get("/:id", (req, res) => {
  res.send(req.params.id);
});
```

Used when:
- ID comes from URL
- REST APIs

---

### `req.body`
```js
router.post("/login", (req, res) => {
  const { email, password } = req.body;
  res.json({ email });
});
```

Requires:
```js
app.use(express.json());
```

Without middleware, `req.body` is `undefined`.

---

## 7️⃣ Common Real Errors We Learned From

### ❌ Error: Cannot find module './routes/userRoutes'
**Why it happens**
- Wrong file name
- Wrong folder path
- Missing `module.exports`

📌 This error teaches how Node.js resolves files.

---

### ❌ 404 Not Found
**Why it happens**
- Router not connected using `app.use()`
- Wrong HTTP method
- Wrong URL in Postman

---

## 8️⃣ Why Real Developers Use Router (Final Understanding)
- Clean architecture
- Easier debugging
- Scalable codebase
- Team-friendly structure
- Industry standard (used in all serious backend projects)

Router is not just syntax — it is **how professionals think about backend design**.

---

## 🎯 What I Actually Gained Today
- Clear understanding of **Express Router**
- How routes are separated logically
- How Express handles requests internally
- Why clean structure matters more than speed

---

✍️ *These notes are written as part of my real-world backend learning journey.*
