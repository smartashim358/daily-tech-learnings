# TypeScript Cheat Sheet – Express/Backend Focus

## Table of Contents
1. [Basic Types](#basic-types)
2. [Variables & Constants](#variables--constants)
3. [Functions](#functions)
4. [Optional & Default Parameters](#optional--default-parameters)
5. [Union & Literal Types](#union--literal-types)
6. [Interfaces & Types](#interfaces--types)
7. [Generics](#generics)
8. [Utility Types](#utility-types)
9. [Arrays & Tuples](#arrays--tuples)
10. [Enums](#enums)
11. [Type Assertions](#type-assertions)
12. [Express + TS](#express--ts)
13. [Router + Typed Request Body](#router--typed-request-body)

---

## Basic Types

```ts
let name: string = "Ashim";
let age: number = 22;
let isActive: boolean = true;
let anything: any = "could be anything"; // Avoid in real projects
let unknownValue: unknown = 5;           // safer than any
let nothing: null = null;
let notDefined: undefined = undefined;
```

---

## Variables & Constants

```ts
const pi: number = 3.14; // constant, cannot reassign
let counter: number = 0;  // mutable variable
```

- Use `const` by default
- `let` only if variable changes
- `var` is outdated

---

## Functions

```ts
function add(a: number, b: number): number {
  return a + b;
}

// Arrow function
const multiply = (x: number, y: number): number => x * y;

// Optional parameter
function greet(name?: string) {
  return `Hello ${name || "Guest"}`;
}

// Default parameter
function pow(num: number, exp: number = 2) {
  return num ** exp;
}
```

---

## Union & Literal Types

```ts
let id: string | number;
id = 101;
id = "202";

type Status = "success" | "error" | "loading";
let s: Status = "success"; // only allowed values
```

---

## Interfaces & Types

```ts
type User = {
  name: string;
  isActive: boolean;
  age?: number;  // optional
}

interface Product {
  id: number;
  name: string;
  price: number;
}

const u: User = { name: "Ashim", isActive: true };
const p: Product = { id: 1, name: "Book", price: 250 };
```

---

## Generics

```ts
function identity<T>(value: T): T {
  return value;
}

identity<string>("Hello");
identity<number>(101);

// Generic array
function getFirst<T>(arr: T[]): T {
  return arr[0];
}

// Generic constraint
function logLength<T extends { length: number }>(value: T) {
  console.log(value.length);
}
```

---

## Utility Types

```ts
type User = { name: string; email: string; age: number };

// Partial → all optional
type UpdateUser = Partial<User>;
const update: UpdateUser = { name: "Ashim" };

// Required → all required
type FullUser = Required<Partial<User>>;

// Readonly → cannot modify
type ReadonlyUser = Readonly<User>;

// Pick → select specific keys
type UserName = Pick<User, "name" | "email">;

// Omit → remove keys
type UserWithoutAge = Omit<User, "age">;

// Record → fixed key-value map
type Roles = "admin" | "user";
const permissions: Record<Roles, boolean> = { admin: true, user: false };
```

---

## Arrays & Tuples

```ts
let nums: number[] = [1, 2, 3];
let names: Array<string> = ["Ashim", "Ram"];

let tuple: [string, number] = ["Ashim", 22]; // fixed order
```

---

## Enums

```ts
enum Role {
  Admin = "ADMIN",
  User = "USER",
  Guest = "GUEST"
}

let r: Role = Role.Admin;
```

---

## Type Assertions

```ts
let val: unknown = "hello";
let str: string = val as string;
```

---

## Express + TS (Core Setup)

### 1️⃣ Install Dependencies
```bash
npm install express
npm install -D typescript ts-node-dev @types/node @types/express
```

### 2️⃣ tsconfig.json
```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "CommonJS",
    "rootDir": "./src",
    "outDir": "./dist",
    "strict": true,
    "esModuleInterop": true
  }
}
```

### 3️⃣ src/app.ts
```ts
import express, { Application } from "express";
import userRouter from "./routes/user.route";

const app: Application = express();
app.use(express.json());

app.use("/api/users", userRouter);

export default app;
```

### 4️⃣ src/server.ts
```ts
import app from "./app";

const PORT = 5000;
app.listen(PORT, () => console.log(`Server running on http://localhost:${PORT}`));
```

---

## Router + Typed Request Body Example

### src/routes/user.route.ts
```ts
import { Router, Request, Response } from "express";

type CreateUserBody = { name: string; email: string };

const router = Router();

// GET /api/users
router.get("/", (req: Request, res: Response) => {
  res.json({ message: "Users list" });
});

// GET /api/users/:id
router.get("/:id", (req: Request, res: Response) => {
  const userId = Number(req.params.id); // always string → convert to number if needed
  res.json({ userId });
});

// POST /api/users
router.post("/", (req: Request<{}, {}, CreateUserBody>, res: Response) => {
  const { name, email } = req.body;
  res.json({ name, email });
});

export default router;
```

---

## ✅ Best Practices for Express + TS

1. Always type `req` and `res`
2. Use `Request<Params, ResBody, ReqBody, Query>` generics
3. Separate `app.ts` (config) & `server.ts` (listen)
4. Separate **routes** and **controllers** for scalability
5. Use **utility types** for clean updates
6. Always `app.use(express.json())` for POST/PUT

---



