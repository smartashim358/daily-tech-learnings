# Express.js Backend Development - Learning Notes

## Table of Contents
1. [Introduction to Express.js](#introduction-to-expressjs)
2. [Setting Up the Express Server](#setting-up-the-express-server)
3. [Express Middleware](#express-middleware)
   - [Built-in Middleware](#built-in-middleware)
   - [Custom Middleware](#custom-middleware)
4. [Routing in Express](#routing-in-express)
5. [Project Structure Best Practices](#project-structure-best-practices)
6. [Example Project](#example-project)
7. [Summary](#summary)

---

## Introduction to Express.js
Express.js is a minimal and flexible Node.js web application framework that provides a robust set of features for building web and mobile applications.

- Handles HTTP requests and responses
- Supports routing
- Provides middleware to handle requests
- Easy to scale and maintain

---

## Setting Up the Express Server

```javascript
const express = require('express');
const app = express();
const port = 3030;

// Built-in middleware to parse JSON request bodies
app.use(express.json());

// Simple route
app.get('/', (req, res) => {
  res.send('Hello from Express!');
});

// Start server
app.listen(port, (err) => {
  if (err) console.log(err.message);
  console.log(`Server running at http://localhost:${port}`);
});
```

**Explanation:**
- `express.json()` parses incoming JSON requests.
- `app.get('/', ...)` defines a GET route at the root URL.
- `app.listen()` starts the server.

---

## Express Middleware

Middleware functions have access to the **request** and **response** objects and can modify them or terminate the request-response cycle.

### Built-in Middleware

1. **express.json()** - Parses JSON bodies.
2. **express.urlencoded()** - Parses URL-encoded bodies.

```javascript
app.use(express.urlencoded({ extended: true }));
```

### Custom Middleware

```javascript
// Logger middleware
const logger = (req, res, next) => {
  console.log(`${req.method} ${req.url} at ${new Date().toISOString()}`);
  next();
};

app.use(logger);
```

**Explanation:**
- Middleware executes in order.
- `next()` passes control to the next middleware or route handler.

---

## Routing in Express

```javascript
app.post('/home', (req, res) => {
  console.log(req.body.name);
  res.send(`Hello ${req.body.name}`);
});
```

### Router Modularization

**user.router.js**
```javascript
const express = require('express');
const router = express.Router();
const { getUser, createUser } = require('./user.controller');

router.get('/', getUser);
router.post('/', createUser);

module.exports = router;
```

**user.controller.js**
```javascript
const getUser = (req, res) => {
  res.send('Get all users');
};

const createUser = (req, res) => {
  const { name } = req.body;
  res.send(`User ${name} created`);
};

module.exports = { getUser, createUser };
```

**server.js**
```javascript
const express = require('express');
const app = express();
const userRouter = require('./user.router');

app.use(express.json());
app.use('/users', userRouter);

app.listen(3030, () => console.log('Server running'));
```

**Why split controllers and routers?**
- **Separation of concerns:** Router defines endpoints; controller defines logic.
- Easier to maintain and scale larger projects.

---

## Project Structure Best Practices

```
project/
│
├─ server.js              # Entry point
├─ package.json
├─ controllers/           # All business logic
│   └─ user.controller.js
├─ routes/                # All route definitions
│   └─ user.router.js
├─ middlewares/           # Custom middleware
│   └─ logger.js
└─ models/                # Database models (if using DB)
```

**Explanation:**
- Modular and scalable structure used in professional projects.

---

## Example Project

### server.js
```javascript
const express = require('express');
const app = express();
const port = 3030;
const userRouter = require('./routes/user.router');

// Middleware
const logger = require('./middlewares/logger');
app.use(logger);
app.use(express.json());

// Routes
app.use('/users', userRouter);

app.listen(port, () => console.log(`Server running at http://localhost:${port}`));
```

### middlewares/logger.js
```javascript
module.exports = (req, res, next) => {
  console.log(`[${new Date().toISOString()}] ${req.method} ${req.url}`);
  next();
};
```

---

## Summary
- Express.js is minimal yet powerful for backend development.
- Middleware handles requests before routes.
- Modular structure with controllers, routers, and middleware is best practice.
- Custom middleware can log requests or handle authentication.

**Next Steps:**
1. Learn error-handling middleware.
2. Connect Express to MongoDB or another database.
3. Implement JWT authentication.
4. Use async/await for asynchronous operations.

---

```
```

