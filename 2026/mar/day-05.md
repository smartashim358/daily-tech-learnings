# Process in Operating System

**Last Updated:** 27 Jan, 2026

---

# 1. What is a Process?

A **Process** is a **program in execution**.

Example workflow:


C/C++ Program (source code)
↓
Compiler
↓
Binary / Executable
↓
Execution
↓
Process


- When we write code → it is a **program**
- When the program **runs in memory** → it becomes a **process**

### Key Idea

| Program | Process |
|------|------|
| Passive entity | Active entity |
| Stored on disk | Running in memory |
| Static | Dynamic |

Example:


Open same application multiple times

Program (.exe)
↓
Run 1 → Process 1
Run 2 → Process 2
Run 3 → Process 3


A **single program can create multiple processes**.

---

# 2. Process Memory Layout

When a process runs, it is divided into **different memory sections**.

    High Memory
    ┌───────────────┐
    │     Stack     │
    │---------------│
    │               │
    │               │
    │     Heap      │
    │               │
    │---------------│
    │   Data Area   │
    │ (Global Var)  │
    │---------------│
    │   Text Area   │
    │ (Program Code)│
    └───────────────┘
    Low Memory

---

## 2.1 Text Section (Code Segment)

- Contains **program instructions**
- Executable code
- Usually **read-only**

Example:

main()
printf()
functions
compiled instructions


---

## 2.2 Data Section

Stores **global and static variables**

Example:


int global = 10;
static int count;


---

## 2.3 Heap Section

- Used for **dynamic memory allocation**
- Memory allocated **during runtime**

Example:


malloc()
calloc()
new (C++)


Heap growth:


Program running
↓
Dynamic allocation
↓
Heap expands upward


---

## 2.4 Stack Section

Used for **temporary data**

Contains:

- Function parameters
- Return addresses
- Local variables

Example:


void func() {
int a = 5; ← stored in stack
}


Stack behavior:


Function Call
↓
Push data to stack
↓
Function Return
↓
Pop data from stack


---

# 3. Attributes of a Process

The operating system keeps information about each process in a structure called:

## Process Control Block (PCB)


Process
↓
Operating System
↓
Process Control Block (PCB)
↓
Stores all process information


---

# 4. Information Stored in PCB

    ┌─────────────────────────┐
    │  Process Control Block  │
    ├─────────────────────────┤
    │ Process ID (PID)        │
    │ Process State           │
    │ CPU Scheduling Info     │
    │ I/O Information         │
    │ File Descriptors        │
    │ Accounting Info         │
    │ Memory Management Info  │
    └─────────────────────────┘

---

## 4.1 Process ID (PID)

- Unique number assigned to each process.

Example:


Process A → PID 101
Process B → PID 102
Process C → PID 103


---

## 4.2 Process State

Shows the **current condition** of the process.

Common states:

  +-------+
  | New   |
  +-------+
      ↓
  +-------+
  | Ready |
  +-------+
      ↓
  +---------+
  | Running |
  +---------+
    ↓     ↓

+--------+ |
|Waiting | |
+--------+ |
↓ |
+--------+
| Ready |
+--------+
↓
+----------+
| Terminated|
+----------+


---

## 4.3 CPU Scheduling Information

Helps OS decide **which process runs next**.

Includes:

- Priority
- Scheduling queue pointers
- CPU registers

---

## 4.4 I/O Information

Information about devices used by the process.

Examples:


Keyboard
Mouse
Disk
Printer
Network


---

## 4.5 File Descriptors

Information about **open files and network connections**.

Example:


File1.txt
Database connection
Socket connection


---

## 4.6 Accounting Information

Tracks **resource usage**.

Examples:

- CPU time used
- Execution time
- Process owner
- Resource limits

---

## 4.7 Memory Management Information

Details about **memory used by the process**.

Includes:


Base address
Limit registers
Page tables
Memory segments
Stack location
Heap location


---

# 5. Summary


Program (Passive)
↓
Execution
↓
Process (Active)
↓
Stored & managed by OS
↓
Information stored in PCB


Process memory layout:


Stack → Function calls
Heap → Dynamic memory
Data → Global variables
Text → Program code


---

# Quick Exam Definition

**Process:**  
A process is a **program in execution**, containing program code, current activity, and system resources managed by the operating system.
