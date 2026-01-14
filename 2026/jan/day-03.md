# Day 03 – Tech Learning 🐍
## Python List — Complete Revision Guide

In Python, a **list** is a built-in data structure used to store an **ordered collection of items**. Python lists are very flexible and powerful compared to arrays in other programming languages.

---

## 🔹 Key Features of Lists

- Can contain **duplicate items**
- **Mutable** — items can be modified, replaced, or removed
- **Ordered** — maintains insertion order
- **Index-based** — indexing starts from `0`
- Can store **mixed data types** (int, float, string, boolean, even other lists)

---

## 🧱 Creating a List

### 1️⃣ Using Square Brackets

```python
a = [1, 2, 3, 4, 5]
b = ['apple', 'banana', 'cherry']
c = [1, 'hello', 3.14, True]
```

### 2️⃣ Using `list()` Constructor

```python
a = list((1, 2, 3, 'apple', 4.5))
b = list("GFG")
```

### 3️⃣ Creating Repeated Elements

```python
a = [2] * 5
b = [0] * 7
```

---

## 🎯 Accessing Elements

```python
nums = [10, 20, 30, 40]
nums[0]      # first element
nums[-1]     # last element
```

---

## ✂️ Slicing

```python
nums[1:4]
nums[:3]
nums[::2]
nums[::-1]
```

---

## 🔄 Modifying Lists

```python
nums[1] = 99
```

---

## ➕ Adding Elements

```python
nums.append(40)
nums.insert(1, 15)
nums.extend([50, 60])
```

---

## ➖ Removing Elements

```python
nums.remove(99)
nums.pop()
nums.pop(1)
del nums[0]
nums.clear()
```

---

## 🧠 List Methods

```python
nums.sort()
nums.sort(reverse=True)
nums.reverse()
nums.copy()
nums.index(8)
nums.count(2)
```

---

## 🔁 Looping

```python
for x in nums:
    print(x)
```

```python
for i in range(len(nums)):
    print(nums[i])
```

```python
i = 0
while i < len(nums):
    print(nums[i])
    i += 1
```

---

## ⚡ List Comprehension

```python
squares = [x**2 for x in range(5)]
even = [x for x in range(10) if x % 2 == 0]
```

---

## 🧩 Nested Lists

```python
matrix = [[1, 2, 3], [4, 5, 6]]
matrix[1][2]
```

---

## 🔍 Membership & Length

```python
2 in nums
len(nums)
```

---

## 📊 List vs Tuple

| Feature | List | Tuple |
|-------|------|-------|
| Mutable | Yes | No |
| Speed | Slower | Faster |
| Syntax | `[]` | `()` |

---

## 📚 Book Content Studied Today

<details>
<summary>Click to view book pages</summary>

![Page 1](../images/page1.png)
![Page 2](../images/page2.png)
![Page 3](../images/page3.png)
![Page 4](../images/page4.png)
![Page 5](../images/page5.png)
![Page 6](../images/page6.png)
![Page 7](../images/page7.png)
![Page 8](../images/page8.png)
![Page 9](../images/page9.png)
![Page 10](../images/page10.png)
![Page 11](../images/page11.png)
![Page 12](../images/page12.png)
![Page 13](../images/page13.png)
![Page 14](../images/page14.png)
![Page 15](../images/page15.png)
![Page 16](../images/page16.png)

</details>

---

## ✅ Key Takeaways (Revision Notes)

- Lists are **fundamental** data structures in Python
- **Flexible and mutable**, suitable for most use cases
- Widely used in **AI, ML, Data Science, and Web Development**
- Practice slicing, list methods, and list comprehension regularly

