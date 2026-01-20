# Day-09 Tech Learning
 ## Asynchronous python

## 1. What is Async Python?
Async Python allows your program to handle multiple I/O-bound tasks efficiently
without blocking the main thread.

Async is best for:
- API calls
- Database queries
- File & network I/O
- Backend servers

❌ Not for CPU-heavy tasks.

---

## 2. Blocking vs Non-Blocking

### Blocking Example
```python
import time

def task():
    time.sleep(2)
    print("Done")
```
## None-Blocing(Async) concept:
- Asynchronous programming allows us to execute multiple tasks concurrently, improving performance and responsiveness.

**Features of asynchronous programming:**

- Improves Performance – Handles multiple tasks without waiting for each to complete.
- Non-Blocking I/O – Ideal for tasks like fetching external data or database operations.
- Better User Experience – Reduces delays for users when making API requests.

## async & await Keywords
```python
async def hello():
    return "Hello"

```
- async def defines a coroutine

- Calling it does NOT execute it

- It must be awaited

```python
async def main():
    result = await hello()
    print(result)

```
## Event Loop

- The event loop:

- Runs async tasks

- Switches tasks when waiting

```python
import asyncio

async def main():
    print("Event loop running")

asyncio.run(main())

```
## Async Sleep (Important)
**Blocking**
```python
time.sleep(2)

```
***Non-Blocking**
```python
await asyncio.sleep(2)

```
## Running Multiple Tasks (asyncio.gather)
```python
import asyncio

async def task(name, delay):
    print(f"{name} started")
    await asyncio.sleep(delay)
    print(f"{name} finished")

async def main():
    await asyncio.gather(
        task("Task-1", 2),
        task("Task-2", 2)
    )

asyncio.run(main())

```
## Background Tasks (create_task)
```python
import asyncio

async def background_task():
    await asyncio.sleep(2)
    print("Background done")

async def main():
    asyncio.create_task(background_task())
    print("Main continues")
    await asyncio.sleep(3)

asyncio.run(main())

```
**Used for:**

- Logging

- Notifications

- Webhooks
## Fetching APIs:
```python
import httpx
import asyncio

async def fetch(url):
    async with httpx.AsyncClient() as client:
        response = await client.get(url)
        return response.json()

async def main():
    data = await fetch("https://api.example.com")
    print(data)

asyncio.run(main())

```
# Basic Linux Commands
Linux commands are used to interact with the operating system through the terminal and perform tasks like file management, navigation, and system monitoring. Learning basic Linux commands helps beginners understand how Linux works and use it efficiently for daily tasks.

- Helps beginners understand and use the Linux terminal effectively
- Covers commonly used commands for files, directories, and system tasks
- Useful for students, developers, and system administrators
- Builds a strong foundation for advanced Linux and server management

## 1. ls
The ls command in Linux is used to list files and directories present in the current working directory.

- Displays files and folders in a directory.
- Helps users quickly understand directory contents
Syntax:
   ls [options][directory]

## 2. cd
The cd command in Linux is used to change the current working directory.

- Allows navigation between directories.
- Moves the user to the home directory when used without arguments.
**Syntax:**

   cd directory_name

## 3. mkdir
The mkdir command in Linux is used to create new directories.

- Creates new folders in the file system.
- Helps organize files and directories.
**Syntax:**

   mkdir directory_name

## 4.rmdir
The rmdir command in Linux is used to delete empty directories.

- Removes directories that do not contain files.
- Helps clean up unused folders.
**Syntax:** 

   rmdir directory_name

## 5.cp
The cp command in Linux is used to copy files or directories.

- Copies files from one location to another.
- Useful for creating backups.
**Syntax:**
  
  cp source destination   