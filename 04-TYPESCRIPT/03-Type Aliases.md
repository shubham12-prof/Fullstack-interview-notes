2. Interfaces vs. Type Aliases
   Q1: What is the difference between an Interface and a Type Alias? When should you use each?
   Answer:
   Both are used to define the shape of an object or a contract for your code, but they have distinct structural differences:

Interfaces: Specifically designed to define object shapes. They support declaration merging (if you declare two interfaces with the same name, TypeScript automatically merges their properties). They also support inheritance via extends.

Type Aliases: Can define objects, primitive aliases, unions, intersections, and tuples. They cannot be reopened for declaration merging; they are closed after definition.

TypeScript
// 1. Declaration Merging with Interface
interface User {
name: string;
}
interface User {
age: number;
}
// Code Explanation: The 'User' interface now strictly requires BOTH name and age
const actor: User = { name: "Tom", age: 40 };

// 2. Unions & Intersections with Type Alias
type Status = "pending" | "success" | "failed"; // Union Type
type Point = { x: number } & { y: number }; // Intersection Type
Rule of Thumb: Use interface for public API object definitions and components where extensibility matters. Use type for complex types, unions, tuples, or utility mappings.
