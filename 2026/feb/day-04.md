# TypeScript + Express Notes

## 1️⃣ TypeScript Basics

### Variables & Types
```ts
let age: number = 21;
let name: string = "Ashim";
let isStudent?: boolean; // optional
```

### Arrays & Tuples
```ts
let scores: number[] = [10, 20, 30];
let user: [string, number] = ["Ashim", 21];
```

### Objects & Interfaces
```ts
interface User {
  name: string;
  age: number;
  isStudent?: boolean;
}

let user1: User = { name: "Ashim", age: 21 };
```

### Functions & Types
```ts
function add(a: number, b: number): number {
  return a + b;
}

function greet(name?: string): void {
  console.log(`Hello ${name || "friend"}`);
}
```

### Generics
```ts
function identity<T>(value: T): T {
  return value;
}

let str = identity<string>("Hello");
let num = identity<number>(123);
```

### Classes & Abstraction
```ts
abstract class Animal {
  constructor(public name: string) {}
  abstract makeSound(): void;
}

class Dog extends Animal {
  makeSound() {
    console.log("Woof Woof");
  }
}

const dog = new Dog("Rex");
dog.makeSound();
```

### Union & Literal Types
```ts
let id: string | number;
id = 123;
id = "abc";

let status: "active" | "inactive";
status = "active";
```

### Optional Properties
```ts
interface User {
  name: string;
  age: number;
  isStudent?: boolean;
}

let user1: User = { name: "Ashim", age: 21 };
let user2: User = { name: "Ram", age: 22, isStudent: true };
```

---

## 2️⃣ Express with TypeScript

### Project Setup
```bash
mkdir express-ts-practice
cd express-ts-practice
npm init -y
npm install express
npm install -D typescript ts-node ts-node-dev @types/node @types/express
npx tsc --init
```

### tsconfig.json
```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "rootDir": "./src",
    "outDir": "./dist",
    "strict": true,
    "esModuleInterop": true
  }
}
```

### Folder Structure
```
src/
 ├─ app.ts
 ├─ server.ts
 ├─ routes/
 │    └─ user.routes.ts
 └─ controllers/
      └─ user.controller.ts
```

### Basic Express App (app.ts)
```ts
import express, { Application } from "express";
import userRoutes from "./routes/user.routes";

const app: Application = express();
app.use(express.json());
app.use("/api/users", userRoutes);

export default app;
```

### Server File (server.ts)
```ts
import app from "./app";
const PORT: number = 3000;
app.listen(PORT, () => {
  console.log(`Server running on http://localhost:${PORT}`);
});
```

### Controllers (user.controller.ts)
```ts
import { Request, Response } from "express";
interface UserParams { id: string }
interface CreateUserDTO { name: string; email: string; }

export const getAllUsers = (req: Request, res: Response) => {
  res.json({ success: true, message: "All users route working" });
};

export const getUserById = (req: Request<UserParams>, res: Response) => {
  const userId = req.params.id;
  res.json({ success: true, message: `User ${userId} route working` });
};

export const createUser = (req: Request<{}, {}, CreateUserDTO>, res: Response) => {
  const { name, email } = req.body;
  res.json({ success: true, message: "User created", user: { name, email } });
};
```

### Router (user.routes.ts)
```ts
import { Router } from "express";
import { getAllUsers, getUserById, createUser } from "../controllers/user.controller";

const router = Router();

router.use((req, res, next) => {
  console.log("User router accessed:", req.method, req.path);
  next();
});

router.get("/", getAllUsers);
router.get("/:id", getUserById);
router.post("/", createUser);

export default router;
```

### TypeScript Tips in Express
- Typed request params: `req: Request<UserParams>`
- Typed request body: `req: Request<{}, {}, CreateUserDTO>`
- Typed query: `req: Request<{}, {}, {}, { page?: string }>`

### Running Project
```bash
npx ts-node src/server.ts
# or using npm script
npm run dev
```

### Test Routes
| Method | URL | Description |
|--------|-----|-------------|
| GET    | /api/users | Get all users |
| GET    | /api/users/:id | Get user by ID |
| POST   | /api/users | Create user |

### Notes for Practice
- Separate routes and controllers
- Use TypeScript types for params, body, query
- Use router-level middleware for logging/auth
- Keep folder structure modular and scalable

