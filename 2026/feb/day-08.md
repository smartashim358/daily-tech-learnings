# NestJS + TypeScript — Core Concepts 
---

## 1. Why TypeScript is Mandatory in NestJS

NestJS is built **on top of TypeScript**.  
TypeScript is not optional — it is the foundation.

TypeScript provides:
- **Static typing** (catch errors before runtime)
- **Better code structure**
- **Scalability for large projects**
- **Clear contracts between files (types, interfaces, DTOs)**

NestJS uses TypeScript features such as:
- Classes
- Decorators
- Interfaces
- Generics
- Access modifiers (`public`, `private`, `readonly`)

---

## 2. How NestJS Application Works (Mental Model)

A NestJS app follows this flow:

```
Request
  ↓
Controller (handles HTTP)
  ↓
Service (business logic)
  ↓
Data (DB / memory / external API)
```

Each layer has **one responsibility only**.

---

## 3. Folder Structure (Real Project)

```
src/
├── app.module.ts
├── main.ts
└── users/
    ├── users.controller.ts
    ├── users.service.ts
    ├── dto/
    │   └── create-user.dto.ts
    └── interfaces/
        └── user.interface.ts
```

This structure:
- Scales well
- Is easy to maintain
- Matches real company projects

---

## 4. Controller (users.controller.ts)

### Responsibility
- Handle HTTP requests
- Validate incoming data shape
- Call services

### Example

```ts
import { Controller, Get, Post, Body } from '@nestjs/common';
import { UsersService } from './users.service';
import { CreateUserDto } from './dto/create-user.dto';

@Controller('users')
export class UsersController {
  constructor(private readonly usersService: UsersService) {}

  @Get()
  findAll() {
    return this.usersService.findAll();
  }

  @Post()
  create(@Body() body: CreateUserDto) {
    return this.usersService.create(body);
  }
}
```

Controller **must not**:
- Store data
- Contain business logic

---

## 5. DTO (Data Transfer Object)

### Definition

A **DTO** defines the **exact shape of incoming data**.

It answers:
> What data is allowed to come from the client?

DTOs are **not JSON**, but **TypeScript classes** that describe JSON.

---

### Example: create-user.dto.ts

```ts
export class CreateUserDto {
  name: string;
  email: string;
}
```

Benefits:
- Predictable request body
- Strong typing
- Works with validation later

NestJS **can read JSON directly**,  
but DTOs make data **safe, structured, and scalable**.

---

## 6. Service (users.service.ts)

### Responsibility
- Business logic
- Data handling
- Reusable logic

### Example

```ts
import { Injectable } from '@nestjs/common';
import { CreateUserDto } from './dto/create-user.dto';
import { User } from './interfaces/user.interface';

@Injectable()
export class UsersService {
  private users: User[] = [];

  findAll(): User[] {
    return this.users;
  }

  create(data: CreateUserDto): User {
    const newUser: User = {
      id: Date.now(),
      ...data,
    };

    this.users.push(newUser);
    return newUser;
  }
}
```

---

## 7. Interface (user.interface.ts)

### Definition

An **interface** defines the structure of internal data.

It is used **inside the application**, not for requests.

### Example

```ts
export interface User {
  id: number;
  name: string;
  email: string;
}
```

---

## 8. Understanding the `never[]` Error

### Error

```
Argument of type 'User' is not assignable to parameter of type 'never'
```

### Why It Happens

TypeScript inferred this:

```ts
private users = [];
```

An empty array without a type becomes `never[]`.

### Correct Fix

```ts
private users: User[] = [];
```

Now TypeScript knows what can be pushed.

---

## 9. Moving Files Correctly (CLI)

If you created a file in the wrong folder:

```bash
mkdir users/dto
mv users/create-user.dto.ts users/dto/create-user.dto.ts
```

Clean structure matters in large projects.

---

## 10. Key Rules to Remember

- Controller = HTTP only
- Service = Logic only
- DTO = Input structure
- Interface = Internal data structure
- Always type arrays explicitly
- One file = one responsibility

---

## 11. What to Learn Next (Only One Thing)

**Validation with DTOs**
- `class-validator`
- `ValidationPipe`

This will complete your request → DTO → service pipeline.

---

## Final Note

If you understand this file:
- You can build real NestJS projects
- You are ready to add database + authentication
- You are no longer a tutorial-only learner

Keep building.
