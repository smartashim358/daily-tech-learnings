# TypeScript Basics (Clean Notes)

These notes cover **only the essentials** needed to build a strong TypeScript foundation before moving to frameworks like Express or NestJS.

---

## 1. Variables & Types

TypeScript is JavaScript with type safety.

```ts
let name: string = "Ashim";
let age: number = 21;
let isActive: boolean = true;
```

### Type Inference

```ts
let city = "Kathmandu"; // inferred as string
let score = 90;          // inferred as number
```

Once inferred, the type cannot change.

---

## 2. Optional & Union Types

Optional values are represented using unions.

```ts
let isStudent: boolean | undefined;
```

Union types allow multiple possible types:

```ts
let id: string | number;
id = 1;
id = "abc";
```

---

## 3. Arrays

### Basic Arrays

```ts
let numbers: number[] = [1, 2, 3];
let names: string[] = ["Ashim", "Ram"];
```

### Mixed Type Array (Union)

```ts
let values: (string | number)[] = [1, "two", 3];
```

### Array of Objects

```ts
interface User {
  name: string;
  age: number;
}

let users: User[] = [
  { name: "Ashim", age: 21 },
  { name: "Ram", age: 22 }
];
```

---

## 4. Tuples

Tuples have fixed length and fixed order.

```ts
let user: [string, number] = ["Ashim", 21];
```

---

## 5. Objects & Interfaces

Interfaces define the structure of objects.

```ts
interface User {
  readonly id: number;
  name: string;
  age: number;
  isStudent?: boolean; // optional
}

let user1: User = {
  id: 1,
  name: "Ashim",
  age: 21
};
```

### Key Rules
- `?` → optional property
- `readonly` → cannot be reassigned
- Extra or missing properties cause errors

---

## 6. Nested Objects

```ts
interface Address {
  city: string;
  country: string;
}

interface User {
  name: string;
  age: number;
  address: Address;
}

let user: User = {
  name: "Ashim",
  age: 21,
  address: {
    city: "Kathmandu",
    country: "Nepal"
  }
};
```

---

## 7. How to Run TypeScript Files

```bash
npm init -y
npm install -D typescript ts-node @types/node
```

Run a file:

```bash
npx ts-node src/variables.ts
```

---

## Practice Notes

- One concept per file (`variables.ts`, `arrays.ts`, `objects.ts`)
- Write JavaScript first, then add types
- Avoid `any`
- Use `interface` for object shapes

---


