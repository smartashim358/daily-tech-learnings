# Day-07: Flask Templates & Jinja2

## 1️⃣ What is a Template in Flask?
- Templates are **HTML files** used to show data from Python (Flask) to browser.
- Flask uses **Jinja2** template engine.
- Python handles logic, Templates handle display.

---

## 2️⃣ Folder Structure

```
project/
│
├── app.py
├── static/
│   └── style.css
└── templates/
    ├── base.html
    └── login.html
```

> **Important:**
> All HTML files must be inside the `templates` folder.  
> All CSS/JS/images must be inside the `static` folder.

---

## 3️⃣ base.html (Parent Template)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}My Flask App{% endblock %}</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>
    <h1>My Flask App</h1>
    <hr>
    {% block content %}{% endblock %}
</body>
</html>
```

**Notes:**
- Provides a **common layout**.
- Child templates fill **blocks**: `title`, `content`.

---

## 4️⃣ login.html (Child Template)

```html
{% extends "base.html" %}

{% block title %}
Login
{% endblock %}

{% block content %}
<h2>Login Page</h2>
<p>{{ message }}</p>
<form method="POST">
    <input type="text" name="username" placeholder="Username">
    <br><br>
    <input type="password" name="password" placeholder="Password">
    <br><br>
    <button type="submit">Login</button>
</form>
{% endblock %}
```

**Notes:**
- `{% extends "base.html" %}` → inherit layout.
- `{{ message }}` → display Python variable.
- No `<html>` or `<body>` in child template.

---

## 5️⃣ Flask App Example

```python
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/", methods=['GET', 'POST'])
def login():
    message = ""
    if request.method == "POST":
        username = request.form.get("username")
        password = request.form.get("password")
        if username == "admin" and password == "1234":
            message = f"Welcome {username}!"
        else:
            message = "Invalid credentials"
    return render_template("login.html", message=message)

if __name__ == "__main__":
    app.run(debug=True)
```

**Notes:**
- `request.form.get()` → get data from HTML form.
- `render_template("login.html", message=message)` → send variable to template.
- Methods = `['GET','POST']` for forms.

---

## 6️⃣ Jinja2 Syntax Summary

| Purpose        | Syntax            | Example                  |
|----------------|-----------------|-------------------------|
| Print variable | `{{ }}`          | `{{ username }}`         |
| Logic / loops  | `{% %}`          | `{% if age > 18 %}`      |
| End blocks     | `{% endif %}`    | `{% endfor %}`           |
| Comments       | `{# #}`          | `{# This is a comment #}`|

**Examples:**

```html
{% if logged_in %}
    <p>Welcome back!</p>
{% else %}
    <p>Please login</p>
{% endif %}

<ul>
{% for user in users %}
    <li>{{ user }}</li>
{% endfor %}
</ul>
```

---

## 7️⃣ Key Learnings Today

1. Templates separate **logic (Python)** and **display (HTML)**.
2. `base.html` → parent layout, `login.html` → child content.
3. Jinja2 is used to:
   - Display variables: `{{ variable }}`
   - Run logic: `{% if %}`, `{% for %}`
   - Comment: `{# comment #}`
4. Forms:
   - Use `method="POST"` in HTML.
   - Use `request.form.get()` in Flask to get input.
5. Folder structure is **critical** (`templates/` and `static/`).

