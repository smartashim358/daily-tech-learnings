# 📚 Backend Learning Notes – JWT & Refresh Tokens (2026-02-01)

## Introduction

Today we dived deep into **backend development**, focusing on **JWT, stateless authentication, and refresh tokens**.  
By the end of this session, you should understand:

- How **stateful vs stateless authentication** works  
- The structure and purpose of **JWT / JWS**  
- How to implement **secure login with refresh tokens**  
- How to **protect routes using middleware**  
- Real-world backend project setup principles  

These notes are written like a **backend developer’s guide**, with **examples and code** for practical use.

---

## 1️⃣ Stateful vs Stateless Authentication

### Stateful
- Server **stores session data**  
- Example: traditional login systems

```txt
User → Login → Server stores session
User → Requests → Server checks session
```

**Pros:** Simple, easy logout  
**Cons:** Hard to scale, server memory heavy, sticky sessions needed

---

### Stateless
- Server **stores nothing**, all info is in the token (JWT)  
- Perfect for REST APIs

```txt
User → Login → Server gives JWT
User → Requests → JWT sent → Server verifies token
```

**Pros:** Scalable, fast, stateless  
**Cons:** Logout & token revocation require extra handling  

---

## 2️⃣ JWT vs JWS

- **JWS (JSON Web Signature):** digitally signs data  
- **JWT (JSON Web Token):** a type of JWS containing **header, payload, signature**

### JWT Structure

```txt
header.payload.signature
```

- **Header:** token type + algorithm
```json
{ "alg": "HS256", "typ": "JWT" }
```

- **Payload:** user info (do NOT store password!)
```json
{ "userId": "123", "role": "user" }
```

- **Signature:** cryptographically signs header + payload  
```txt
HMACSHA256(base64(header) + "." + base64(payload), secret_key)
```

---

## 3️⃣ JWT in Node.js (Code Examples)

### Install
```bash
npm install jsonwebtoken
```

### Generate Token (Login)
```js
const jwt = require("jsonwebtoken");

const token = jwt.sign(
  { userId: user._id },
  process.env.JWT_SECRET,
  { expiresIn: "15m" }
);
```

### Protect Routes
```js
const authMiddleware = (req, res, next) => {
  const token = req.headers.authorization?.split(" ")[1];
  if (!token) return res.status(401).json({ message: "No token" });

  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    next();
  } catch {
    res.status(401).json({ message: "Invalid token" });
  }
};
```

---

## 4️⃣ Refresh Tokens (Why & How)

**Problem:** Access tokens are short-lived  
**Solution:** Use **refresh tokens** to get new access tokens without login  

### Token Types

| Token | Stored where | Expiry | Purpose |
|-------|--------------|--------|---------|
| Access | Client memory / headers | 15m | API access |
| Refresh | DB + httpOnly cookie | 7d | Get new access token |

### Code – Generate Access & Refresh Tokens
```js
const jwt = require("jsonwebtoken");

const generateAccessToken = (userId) =>
  jwt.sign({ userId }, process.env.JWT_SECRET, { expiresIn: "15m" });

const generateRefreshToken = (userId) =>
  jwt.sign({ userId }, process.env.JWT_REFRESH_SECRET, { expiresIn: "7d" });

module.exports = { generateAccessToken, generateRefreshToken };
```

### Login Controller
```js
const login = async (req, res) => {
  const user = await User.findOne({ email: req.body.email });
  if (!user) return res.status(401).json({ message: "Invalid credentials" });

  const accessToken = generateAccessToken(user._id);
  const refreshToken = generateRefreshToken(user._id);

  user.refreshToken = refreshToken;
  await user.save();

  res.cookie("refreshToken", refreshToken, { httpOnly: true, sameSite: "strict" });
  res.json({ accessToken });
};
```

### Refresh Token Endpoint
```js
const refreshTokenHandler = async (req, res) => {
  const refreshToken = req.cookies.refreshToken;
  if (!refreshToken) return res.status(401).json({ message: "No refresh token" });

  const user = await User.findOne({ refreshToken });
  if (!user) return res.status(403).json({ message: "Invalid refresh token" });

  jwt.verify(refreshToken, process.env.JWT_REFRESH_SECRET, (err, decoded) => {
    if (err) return res.status(403).json({ message: "Expired refresh token" });

    const newAccessToken = generateAccessToken(decoded.userId);
    res.json({ accessToken: newAccessToken });
  });
};
```

---

## 5️⃣ Full Request Flow (Visual)

```txt
1️⃣ Login → get access + refresh tokens
2️⃣ Access token expires
3️⃣ Client calls /refresh-token
4️⃣ Server validates refresh token
5️⃣ New access token issued
6️⃣ User continues without logging in again
```

---

## 6️⃣ Security Notes

- Access tokens **short-lived** → reduces damage if stolen  
- Refresh tokens **httpOnly + stored in DB** → harder to steal  
- Always use **env variables for secrets**  
- Optional: rotation + blacklist for max security  

---

## 7️⃣ Real-World Project Roadmap

After JWT and refresh tokens, for a backend project:

1. Complete auth (register, login, refresh, logout) 
2. CRUD operations (POST, GET, PUT, DELETE)  
3. Role-based authorization (admin / user)  
4. Security hardening (bcrypt, rate limiting, helmet, etc.)  
5. Project folder structure professional  
6. API documentation (Postman / Swagger)

---

## 8️⃣ Key Takeaways

- **JWT = stateless, scalable auth**  
- **Refresh tokens = extend session safely**  
- Middleware protects routes effortlessly  
- Real backend dev workflow = auth → CRUD → roles → security → docs  
- You’re ready to **start a production-level project**

