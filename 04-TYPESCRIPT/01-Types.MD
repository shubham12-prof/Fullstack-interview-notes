## 1. Types

### Q1: What is the primary difference between Static Typing and Dynamic Typing, and how does TypeScript implement it?

**Answer:**

- **Dynamic Typing (JavaScript):** Types are associated with _values_ at runtime. A variable can hold a number and immediately be reassigned to a string. Errors are only caught when the code executes.
- **Static Typing (TypeScript):** Types are checked at _compile-time_. Variables are bound to specific data types, and the compiler prevents incorrect assignments before the code ever runs.

TypeScript adds a type system to JavaScript, introducing core primitives (`string`, `number`, `boolean`, `any`, `unknown`, `never`, and `void`).

| Type      | Purpose                               | Behavior                                                                                     |
| :-------- | :------------------------------------ | :------------------------------------------------------------------------------------------- |
| `any`     | Turns off type checking completely.   | Allows any operation; dangerous for type safety.                                             |
| `unknown` | A type-safe counterpart to `any`.     | You must narrow the type (using `typeof` or type guards) before performing operations on it. |
| `never`   | Represents values that _never_ occur. | Used for functions that throw errors or enter infinite loops.                                |
| `void`    | Represents the absence of a value.    | Used as the return type for functions that do not return a value.                            |

```typescript
let value: unknown = "Hello World";

// Code Explanation:
// Directly invoking a method on 'unknown' fails compile-time checks:
// value.toUpperCase(); // Error!

if (typeof value === "string") {
  // TypeScript narrows the type to 'string' inside this block safely
  console.log(value.toUpperCase()); // Works perfectly!
}
```
