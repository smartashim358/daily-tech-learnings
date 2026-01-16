# 🧠 Python Sets (Revision)

## What is a Python Set?
A **set** in Python is an **unordered**, **mutable**, and **unindexed** collection of **unique elements**.

### Key Characteristics
- Stores **unique values only** (duplicates are removed automatically)
- **Unordered** → element order is not preserved
- **Mutable** → elements can be added or removed
- **Unindexed** → no access via index (`set[0]` ❌)
- Can store `None`
- Implemented internally using **hash tables**
- **Not thread‑safe** by default (needs synchronization in multi‑threading)

---

## Creating a Set

### Using Curly Braces (Recommended)
```python
thisset = {"apple", "ball", "cat", "dog"}
print(thisset)
```
**Output (order may vary):**
```
{'cat', 'apple', 'dog', 'ball'}
```

### Empty Set
```python
empty_set = set()   # Correct
```
❌ `{}` creates a dictionary, not a set.

---

## Duplicates Not Allowed
Duplicate values are ignored automatically.

```python
thisset = {"apple", "ball", "cat", "dog", "apple"}
print(thisset)
```
**Output:**
```
{'apple', 'cat', 'ball', 'dog'}
```

---

## Length of a Set
```python
thisset = {"apple", "ball", "cat", "dog"}
print(len(thisset))
```
**Output:**
```
4
```

---

## Unordered, Unindexed & Mutable
- Order may change on every run
- No indexing support
- Elements can be added or removed

```python
set1 = {3, 1, 4, 1, 5, 9, 2}
print(set1)
```

### Indexing is NOT allowed
```python
try:
    print(set1[0])
except TypeError as e:
    print(e)
```
**Output:**
```
'set' object is not subscriptable
```

---

## Boolean Values in Sets (Important ⚠️)

`True == 1` and `False == 0` in Python.

```python
thisset = {"apple", "banana", "cherry", True, 1, 2}
print(thisset)
```
**Output:**
```
{'banana', 2, True, 'apple', 'cherry'}
```

```python
thisset = {"apple", "banana", "cherry", False, True, 0}
print(thisset)
```
**Output:**
```
{False, True, 'banana', 'apple', 'cherry'}
```

---

## Using the `set()` Constructor
```python
thisset = set(("apple", "banana", "cherry"))
print(thisset)
```

---

## Accessing Set Items
You **cannot access items by index**, but you can:
- Loop through items
- Check membership

### Looping
```python
thisset = {"apple", "banana", "cherry"}
for x in thisset:
    print(x)
```

### Membership Check
```python
print("banana" in thisset)   # True
print("mango" in thisset)    # False
```

---

## Adding Items

### add()
```python
thisset.add("orange")
```

### update() with another set
```python
thisset = {"apple", "banana", "cherry"}
tropical = {"pineapple", "mango", "papaya"}
thisset.update(tropical)
print(thisset)
```

### update() with any iterable
```python
mylist = ["kiwi", "orange"]
thisset.update(mylist)
```

---

## Removing Items

### remove() → Error if not found
```python
thisset.remove("banana")
```

### discard() → No error if missing
```python
thisset.discard("banana")
```

### pop() → Removes random item
```python
x = thisset.pop()
print(x)
print(thisset)
```

### clear() → Empties set
```python
thisset.clear()
print(thisset)
```

### del → Deletes set completely
```python
del thisset
```

---

## Set Operations (VERY IMPORTANT 🔥)

### Union
```python
a = {1, 2, 3}
b = {3, 4, 5}
print(a | b)
```

### Intersection
```python
print(a & b)
```

### Difference
```python
print(a - b)
```

### Symmetric Difference
```python
print(a ^ b)
```

---

## Subset & Superset
```python
a = {1, 2}
b = {1, 2, 3, 4}

print(a.issubset(b))     # True
print(b.issuperset(a))   # True
```

---

## Set Methods vs Operators

| Operation | Operator | Method |
|--------|--------|--------|
| Union | `a | b` | `a.union(b)` |
| Intersection | `a & b` | `a.intersection(b)` |
| Difference | `a - b` | `a.difference(b)` |
| Symmetric Difference | `a ^ b` | `a.symmetric_difference(b)` |

## Video reference:
## Python set:
[![Python set](https://img.youtube.com/vi/gOMW_n2-2Mw/0.jpg)](https://www.youtube.com/watch?v=gOMW_n2-2Mw)


