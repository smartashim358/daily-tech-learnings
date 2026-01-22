# Day 11 of tech learning
## HTTP Request & Response -- Flask Backend Fundamentals
-----------------------------------------------------------------
## 1. What is HTTP?

HTTP (HyperText Transfer Protocol) is a rulebook that defines how a
client (browser/app) communicates with a server.

Client sends a REQUEST → Server sends a RESPONSE.

------------------------------------------------------------------------

## 2. HTTP Request (Deep Concept)

An HTTP request contains: 1. Method -- What action to perform 2. Path --
Which resource 3. Headers -- Metadata (auth, content type, etc.) 4. Body
-- Data sent to server (optional)

### Example:

POST /login\
Headers: Authorization, Content-Type\
Body: JSON data

------------------------------------------------------------------------

## 3. HTTP Methods (Meaning)

-   GET -- Read data
-   POST -- Create data
-   PUT -- Replace data
-   PATCH -- Update part of data
-   DELETE -- Remove data

Rule: GET should never change server state.

------------------------------------------------------------------------

## 4. HTTP Response (Deep Concept)

A response contains: 1. Status Code -- Result of request 2. Headers --
Metadata 3. Body -- Data returned

------------------------------------------------------------------------

## 5. Status Codes (Backend Language)

-   200 OK
-   201 Created
-   400 Bad Request
-   401 Unauthorized
-   403 Forbidden
-   404 Not Found
-   500 Server Error

------------------------------------------------------------------------

## 6. Flask Basic Request Handling

``` python
@app.route("/")
def home():
    return "Hello HTTP"
```

Client sends GET /\
Server responds with 200 OK

------------------------------------------------------------------------

## 7. Request Object in Flask

Flask stores incoming request info in `request`.

Common attributes: - request.method - request.path - request.args -
request.headers - request.json

------------------------------------------------------------------------

## 8. Query Parameters (request.args)

URL: `/search?query=python&page=2`

Code:

``` python
query = request.args.get("query")
page = request.args.get("page")
```

Safe reading using `.get()` (returns None if missing).

------------------------------------------------------------------------

## 9. Request Body (JSON)

Client sends JSON data.

``` python
data = request.json
email = data.get("email")
```

Used in POST/PUT requests.

------------------------------------------------------------------------

## 10. Headers (Metadata)

Headers carry extra information, not main data.

Common headers: - Authorization - Content-Type - User-Agent

Reading Authorization header:

``` python
auth = request.headers.get("Authorization")
```

------------------------------------------------------------------------

## 11. Authorization Header

Used for authentication tokens (JWT).

Format: Authorization: Bearer `<token>`{=html}

Backend must read → validate → verify.

------------------------------------------------------------------------

## 12. Response in Flask

Returning dict automatically becomes JSON.

``` python
return {"message": "success"}, 200
```

Flask sets Content-Type and status code.

------------------------------------------------------------------------

## 13. Backend Request Flow (Mental Model)

1.  Read request
2.  Validate data
3.  Authenticate user
4.  Apply business logic
5.  Access database
6.  Return response

------------------------------------------------------------------------

## 14. Key Principles to Remember

-   Never trust client input
-   Use correct HTTP methods
-   Use proper status codes
-   Headers ≠ Body
-   Reading token ≠ trusting token

------------------------------------------------------------------------

## 15. One-Line Summary

HTTP is message-based communication.\
Backend reads requests, applies rules, and sends structured responses.

This foundation applies to Flask, FastAPI, Django, Node.js, and all
backend frameworks.
--------------------------------------------------------------

# Express.js Backend Core Concepts 🚀

This document covers **core backend concepts using Express.js**, written for **deep understanding** and **GitHub-ready documentation**.

---

## 1. What is Express.js?
Express.js is a **minimal Node.js web framework** built on top of the native `http` module.

**Why Express?**
- Lightweight
- No magic / low abstraction
- Perfect for learning backend fundamentals

---

## 2. Request → Response Lifecycle

```
Client
  ↓
Request (req)
  ↓
Middleware
  ↓
Route Handler
  ↓
Response (res)
  ↓
Client
```

> Everything in Express is middleware.

---

## 3. Minimal Express Server

```js
const express = require("express");

const app = express();

// Global middleware
app.use(express.json());

app.get("/", (req, res) => {
  res.status(200).send("Express backend started 🚀");
});

app.listen(3000, () => {
  console.log("Server running on http://localhost:3000");
});
```

Run the server:
```bash
node index.js
```

---

## 4. Understanding `req` (Request Object)

`req` contains all client-side information.

### Common properties:
- `req.method`
- `req.url`
- `req.headers`
- `req.body`
- `req.query`
- `req.params`

### Example:
```js
app.get("/user/:id", (req, res) => {
  console.log(req.params); // { id: "123" }
  console.log(req.query);  // ?name=ashim
  res.send("OK");
});
```

---

## 5. Understanding `res` (Response Object)

You control:
- Status code
- Headers
- Response body

```js
res.status(201).json({ message: "User created" });
```

---

## 6. Middleware (CORE CONCEPT)

Middleware is a function that runs **before the route handler**.

```js
app.use((req, res, next) => {
  console.log("Request received");
  next();
});
```

⚠️ Without calling `next()`, the request will be blocked.

---

## 7. Route-level Middleware (Auth Example)

```js
function auth(req, res, next) {
  const token = req.headers.authorization;
  if (!token) {
    return res.status(401).json({ error: "Unauthorized" });
  }
  next();
}

app.get("/dashboard", auth, (req, res) => {
  res.send("Welcome to dashboard");
});
```

---

## 8. HTTP Status Codes (Must Know)

| Code | Meaning |
|----|----|
| 200 | OK |
| 201 | Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |

---
