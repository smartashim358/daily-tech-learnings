# Python Variables & Dictionary (Revision with Backend overview)

## 🎯 Goal of today:
By the end of this day, we shall:
- Understand variables as **real backend system state**
- Use `if`, `continue`, and `break` correctly
- Build a **secure login attempt logic**
- Think like a **backend engineer**

---

## 1️⃣ Variables in Backend (Real Meaning)

❌ simple definition:  
> Variable is a container to store data

✅ Backend definition:  
> **A variable represents REAL SYSTEM STATE**

Examples:
- Logged-in user
- Login attempts
- Tokens
- Money
- API request data

```python
user_id = 1
username = "ashim"
is_authenticated = False
```

---

## 2️⃣ Backend-Style Variable Naming

❌ Bad
```python
x = 10
a = "test"
```

✅ Good
```python
user_id = 10
email_address = "test@gmail.com"
http_status_code = 200
```

📌 Rule:  
If another developer can’t understand your variable → ❌ reject code

---

## 3️⃣ Real Backend Variable Examples

### 👤 User Data
```python
user_name = "Ashim"
user_email = "ashim@gmail.com"
is_email_verified = False
```

### 🔐 Authentication
```python
access_token = "jwt_token"
token_expiry_seconds = 3600
is_authenticated = True
```

### 🌐 API Request Data
```python
request_data = {
    "username": "ashim",
    "password": "1234"
}
```

---

## 4️⃣ Variable Types Used in Backend

| Type | Example | Usage |
|----|----|----|
| int | `user_id = 1` | IDs, counts |
| float | `price = 99.99` | Money |
| str | `"email"` | Text |
| bool | `True` | Status |
| dict | `{}` | API / DB |
| list | `[]` | Multiple records |

---

## 5️⃣ Login System (Max 5 Attempts)

### 🔒 Rules:
- Username cannot be empty
- Password must be at least 4 characters
- User can try only 5 times

```python
MAX_LOGIN_ATTEMPTS = 5
login_attempts = 0

CORRECT_USERNAME = "admin"
CORRECT_PASSWORD = "1234"

while login_attempts < MAX_LOGIN_ATTEMPTS:
    username = input("Enter username: ").strip()
    password = input("Enter password: ").strip()

    # validation
    if not username:
        print("❌ Username cannot be empty")
        continue

    if len(password) < 4:
        print("❌ Password must be at least 4 characters")
        continue

    # authentication
    if username == CORRECT_USERNAME and password == CORRECT_PASSWORD:
        print("✅ Login successful")
        break
    else:
        login_attempts += 1
        remaining = MAX_LOGIN_ATTEMPTS - login_attempts
        print(f"❌ Invalid credentials. Attempts left: {remaining}")

if login_attempts == MAX_LOGIN_ATTEMPTS:
    print("🚫 Account locked. Too many login attempts.")
```

---

## 6️⃣ `continue` vs `break` (Backend Logic)

### 🟡 `continue`
> Kill current request, allow retry

```python
if not username:
    continue
```

Backend meaning:
- Validation failed
- Reject request
- User can try again

---

### 🔴 `break`
> Stop the process completely

```python
if login_success:
    break
```

Backend meaning:
- Login success
- Account locked
- Final state reached

---

## 7️⃣ Important Correction

❌ Wrong idea:
> `break` restarts loop from zero

✅ Correct:
> `break` **exits the loop forever**

---

## 8️⃣ Visual Flow

### `continue`
```
while running:
  ❌ invalid input
  continue
↺ try again
```

### `break`
```
while running:
  ✅ success
  break
⬇ exit loop
```

---

## 9️⃣ Security Rule (VERY IMPORTANT)

❌ Never hardcode secrets:
```python
SECRET_KEY = "mysecret"
```

✅ Use environment variables:
```python
import os
SECRET_KEY = os.getenv("SECRET_KEY")
```

---

## 🧠 Backend Golden Rules (today:2026/01/17)

- Variables = system state
- Validate early
- Use `continue` for bad input
- Use `break` for final state
- Never trust user input
- Clean variable naming is mandatory

---
# Python Dictionary ( Revision & Backend Focus)

## What is a Dictionary?
A dictionary is a **key-value** data structure used to store related data.
In backend development, dictionaries are heavily used to represent:
- Users
- JSON data
- Database-like structures
- API request/response data

---

## Creating a Dictionary
```python
user = {
    "username": "admin",
    "password": "1234",
    "is_active": True
}
```

---

## Accessing Dictionary Values
```python
print(user["username"])
```

⚠️ If the key does not exist, it will raise an error.

Safe way:
```python
print(user.get("username"))
```

---

## Real Backend Example: User Database
```python
user_db = {
    "admin": {
        "password": "1234",
        "role": "superadmin"
    },
    "john": {
        "password": "abcd",
        "role": "user"
    }
}
```

---

## Important Line Explained
```python
user = user_db[username]
```

### Meaning:
- `username` is entered by the user
- `user_db[username]` fetches that user's data
- `user` becomes a dictionary

Example:
```python
username = "admin"
user = user_db["admin"]

print(user["password"])  # 1234
```

---

## Login Validation Using Dictionary
```python
username = input("Username: ")
password = input("Password: ")

if username in user_db:
    user = user_db[username]
    if user["password"] == password:
        print("Login successful")
    else:
        print("Wrong password")
else:
    print("User not found")
```

---

## Why Dictionary is IMPORTANT for Backend
- Represents database rows
- Works directly with JSON
- Fast lookup (O(1))
- Clean and readable code

---

## Common Dictionary Methods
```python
user.keys()
user.values()
user.items()
```

---

## Summary
- Dictionary = backend backbone
- Used everywhere (Django, Flask, APIs)
- Maps directly to real-world data




