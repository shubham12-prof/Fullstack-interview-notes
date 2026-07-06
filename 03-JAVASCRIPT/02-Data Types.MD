## Q1: What are JavaScript's primitive data types, and how do they differ from Objects?

Answer:
JavaScript features 7 primitive data types: string, number, boolean, undefined, null, symbol, and bigint. Anything else is an object (including arrays and functions).

Primitives: Immutably stored by value. Modifying a variable creates a new value in memory space.

Objects: Stored by reference. Multiple variables can point to the exact same memory location, meaning modifying an object property via one variable updates it for all references.

JavaScript
// Primitive behavior (by value)
let a = 10;
let b = a;
b = 20; // Changing b does NOT change a

// Object behavior (by reference)
let obj1 = { name: "Alice" };
let obj2 = obj1;
obj2.name = "Bob";

// Code Explanation:
console.log(obj1.name); // Outputs "Bob" because obj1 and obj2 point to the same memory sl
