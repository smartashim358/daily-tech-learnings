# 🟢 JavaScript for Backend Cheat Sheet

This cheat sheet covers the **essential JavaScript concepts** you must master for Node.js backend development.

---

## 1️⃣ Async / Await & Promises
- **Use** for DB calls, API requests, bcrypt, JWT, file I/O.
- **Syntax:**
```js
const user = await User.findOne({ email });
const hashed = await bcrypt.hash(password, 10);
```
- **Tip:** Always wrap async code in `try/catch`.

---

## 2️⃣ Modules (require / import)
- **Use** to organize routes, controllers, models, middleware.
```js
const express = require("express");
const authRoutes = require("./routes/auth.route");
```
- **Tip:** Keep backend modular and maintainable.

---

## 3️⃣ Objects & Destructuring
- **Use** for JSON, request bodies, JWT payloads.
```js
const { email, password } = req.body;
const { userId } = jwt.verify(token, process.env.JWT_SECRET);
```

---

## 4️⃣ Functions & Arrow Functions
- **Use** for controllers, middleware, helpers.
```js
const auth = (req, res, next) => { ... }
```
- Arrow functions preserve `this` context.

---

## 5️⃣ Template Strings
- **Use** for dynamic logs, messages, URLs.
```js
console.log(`User ${email} logged in at ${new Date()}`);
```

---

## 6️⃣ Error Handling & Throwing
- **Never let your server crash.** Handle errors gracefully.
```js
if(!user) throw new Error("User not found");
```
- Wrap async calls in `try/catch`.

---

## 7️⃣ Array & Object Methods
- `.map()`, `.filter()`, `.find()`, `.reduce()`
- **Use** for data manipulation.
```js
const admins = users.filter(u => u.role === "admin");
```

---

## 8️⃣ Environment Variables
- **Use** for secrets, DB URIs, JWT keys.
```js
const token = jwt.sign(payload, process.env.JWT_SECRET);
```
- **Tip:** Always keep `.env` secret.

---

## ⚡ Example: Real Backend Code
```js
const registerUser = async (req, res) => {
  try {
    const { name, email, password } = req.body;
    const hashed = await bcrypt.hash(password, 10);
    const user = await User.create({ name, email, password: hashed });
    const token = jwt.sign({ userId: user._id }, process.env.JWT_SECRET);
    res.status(201).json({ user, token });
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
};
```

Every line above uses JS core skills for backend!

---

## ✅ Priority Summary Table
| Concept | Importance | Use Case |
|---------|-----------|---------|
| Async / Await & Promises | 🔥 Critical | DB calls, bcrypt, JWT |
| Modules | 🔥 Critical | Organize backend code |
| Objects & Destructuring | 🔥 Critical | req.body, DB, JWT |
| Functions & Arrow | 🔥 High | Middleware, controllers |
| Template Strings | ⭐ Useful | Logs, dynamic responses |
| Error Handling | 🔥 Critical | Server stability |
| Array/Object Methods | ⭐ High | Data manipulation |
| Env Variables | 🔥 Critical | Secrets, DB URIs |

---

> Master these and you can confidently handle **any Node.js backend project**.

