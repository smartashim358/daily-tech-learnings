
# NestJS DTO Validation – Clean Notes

## 1. Why Validation Matters in Backend Development

In real-world backend systems, APIs must protect themselves from invalid or malicious input.
NestJS provides a structured validation system that runs before controller and service logic.

Without validation:
- Invalid data reaches business logic
- Databases get polluted
- Security risks increase

Validation ensures only correct data enters the system.

---

## 2. Where Validation Lives in NestJS

Validation is registered globally inside `main.ts`.

Reason:
- `main.ts` runs once at application startup
- Global configuration avoids repetition
- Ensures consistent behavior across all routes

```ts
app.useGlobalPipes(new ValidationPipe());
```

---

## 3. What Is a Pipe in NestJS

A Pipe is a function that runs before the controller.

Request flow:

Client Request → Pipe → Controller → Service

Validation happens before business logic, which is correct architecture.

---

## 4. ValidationPipe Explained Line by Line

```ts
app.useGlobalPipes(
  new ValidationPipe({
    whitelist: true,
    forbidNonWhitelisted: true,
    transform: true,
  }),
);
```

### whitelist: true
Removes properties not defined in the DTO.

Why it matters:
- Prevents extra data
- Keeps request payload clean

---

### forbidNonWhitelisted: true
Throws an error instead of silently removing extra fields.

Why it matters:
- Enforces strict API contracts
- Improves security

---

### transform: true
Transforms plain JSON into a real DTO class instance.

Why it matters:
- Enables proper type conversion
- Prevents hidden bugs

---

## 5. Why DTO Must Be a Class

DTOs must be classes, not types or interfaces.

Decorators require runtime metadata, which only classes provide.

---

## 6. Controller Using DTO

```ts
@Post()
create(@Body() createUserDto: CreateUserDto) {
  return createUserDto;
}
```

The controller receives safe, validated data.

---

## 7. Request Lifecycle Summary

Request → ValidationPipe → Controller → Service

If validation fails, the request stops early.

---

## 8. Professional Backend Principle

- DTO defines contract
- ValidationPipe enforces contract
- Controller handles request
- Service contains business logic

---

## 9. Conclusion

DTO validation is mandatory for real NestJS projects.
