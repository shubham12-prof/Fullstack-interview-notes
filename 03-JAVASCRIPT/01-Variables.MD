# JavaScript Interview Preparation Guide

---

## 1. Variables

### Q1: What is the difference between `var`, `let`, and `const`?

**Answer:**
The differences boil down to three main criteria: **scope**, **hoisting**, and **re-assignment**.

| Feature           | `var`                    | `let`                         | `const`                       |
| :---------------- | :----------------------- | :---------------------------- | :---------------------------- |
| **Scope**         | Function Scoped          | Block Scoped `{}`             | Block Scoped `{}`             |
| **Hoisting**      | Hoisted with `undefined` | Hoisted in Temporal Dead Zone | Hoisted in Temporal Dead Zone |
| **Re-assignment** | Allowed                  | Allowed                       | Not Allowed                   |
| **Redeclaration** | Allowed                  | Not Allowed                   | Not Allowed                   |

```javascript
function testScope() {
  if (true) {
    var functionScoped = "I am visible everywhere in this function";
    let blockScoped = "I am only visible inside this if block";
  }
  // Code Explanation:
  console.log(functionScoped); // Works because var ignores the if-block boundaries
  console.log(blockScoped); // ReferenceError: blockScoped is locked to its block
}
```
