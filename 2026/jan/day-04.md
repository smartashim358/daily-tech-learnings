# Day 04 – Python File Handling & Git Commands (Revision)

## 📅 Topics Covered
- Python File Handling (Read, Write, Append)
- Best practices using `with`
- Real-world use cases
- Git commands revision (including pull, clone, push, commit, etc.)

---

## 🐍 Python File Handling

File handling allows programs to store data permanently and interact with real-world systems.
This is essential for AI, backend development, automation, cybersecurity, and robotics.

---

## 📂 Opening a File

### Syntax
```python
open("filename", "mode")
```

### File Modes
| Mode | Description |
|----|------------|
| `r` | Read (default) |
| `w` | Write (overwrite file) |
| `a` | Append (add data) |
| `r+` | Read + Write |

---

## ✍️ Writing to a File (`w` mode)

```python
with open("readfile1.txt", "w") as f:
    f.write("From the adjoining mapping diagram, write the pre-images of q\n")
```

---

## ➕ Appending to a File (`a` mode)

```python
with open("readfile1.txt", "a") as f:
    f.write("In how many places a vertical line cuts the function\n")
```

---

## 📖 Reading from a File

```python
with open("readfile1.txt", "r") as f:
    print(f.read())
```

---

## 🔁 Git Commands Revision

### Initialize Repository
```bash
git init
```

### Clone Repository
```bash
git clone <repository_url>
```

### Check Status
```bash
git status
```

### Add Files
```bash
git add .
```

### Commit
```bash
git commit -m "Day 04: File handling and git commands"
```

### Push
```bash
git push origin main
```

### Pull
```bash
git pull origin main
```

### Branch
```bash
git branch
```

### Log
```bash
git log
```

---
## Video reference for learning:
**File handling:**
[![Video Title](https://img.youtube.com/vi/aequTxAvQq4/0.jpg)](https://www.youtube.com/watch?v=aequTxAvQq4)
-----------------------------------------------------------------------------------------------------------------
**Git Command:**
[![Video Title](https://img.youtube.com/vi/rE2zRhZdjFU/0.jpg)](https://www.youtube.com/watch?v=rE2zRhZdjFU)


