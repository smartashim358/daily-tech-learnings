# TypeScript – Day Notes (Basics)


---

## 1. Why TypeScript
TypeScript adds **type safety** to JavaScript. Errors are caught **before runtime**.

---

## 2. Variables in TypeScript

### Basic Types
```ts
let name: string = "Ashim";
let age: number = 21;
let isStudent: boolean = true;
```

### Type Inference
TypeScript can guess types automatically.
```ts
let city = "Kathmandu"; // string
let score = 100;         // number
```
Once inferred, the type cannot change.

---

## 3. const vs let
```ts
const country: string = "Nepal"; // cannot change
let level: number = 1;            // can change
```

---

## 4. Union Types
A variable can have **more than one type**.
```ts
let userId: number | string;
userId = 101;
userId = "A101";
```
Used a lot in backend (IDs, params).

---

## 5. any (use carefully)
```ts
let data: any = 10;
data = "hello";
data = true;
```
Avoid unless data type is truly unknown.

---

## 6. Functions in TypeScript

### Basic Function
```ts
function add(a: number, b: number): number {
  return a + b;
}
```

### Void Function
```ts
function log(msg: string): void {
  console.log(msg);
}
```

### Arrow Function
```ts
const greet = (name: string): string => {
  return `Hi ${name}`;
};
```

---

## 7. Optional Parameters
```ts
function welcome(name: string, age?: number): string {
  return age ? `Welcome ${name}, age ${age}` : `Welcome ${name}`;
}
```

---

## 8. Type Alias (Core Concept)

### Defining a Type
```ts
type User = {
  name: string;
  isActive: boolean;
};
```

- `type` is a **rule / blueprint**
- It does NOT create data
- Used only for type checking

---

## 9. Using Type in Functions
```ts
function createUser(user: User): User {
  return user;
}
```

Meaning:
- Function **accepts** a User
- Function **returns** a User
- Missing or wrong fields cause TS error

Valid:
```ts
createUser({ name: "Ashim", isActive: true });
```

Invalid:
```ts
createUser({ name: "Ashim" }); // error
```

---

## 10. Mental Model
```
Type  → rule
Function input → must follow rule
Function output → must follow rule
```

---

## 11. How to Run TS Files
```bash
npx ts-node src/filename.ts
```

---

## 12. Practice Folder Structure
```
Ts_Learn/
 ├─ src/
 │   ├─ variables.ts
 │   ├─ functions.ts
 │   └─ practice.ts
 ├─ tsconfig.json
 └─ package.json
```

---
## code for practice:
```ts
interface User{
    id:number;
    name:string;
    email?:string;
    isActive:boolean;
    role?:"admin"|"user"|"guest";
}
interface Admin extends User{
    permissions:string[];
}
const currentUser:User = {
    id:1001,
    name:"ashim nepali",
    isActive:true,
    role:"admin"
};
console.log("currentuser is", currentUser);
const superUser:Admin = {
    id:1002,
    name:"ram kumar",
    isActive:true,
    role:"admin",
    permissions:["delete","ban","everything"]
};
console.log(`supers is ${superUser}`);
```
✅ End of today’s TypeScript basics

