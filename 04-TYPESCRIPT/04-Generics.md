3. Generics
   Q1: What are Generics, and how do they help create reusable components?
   Answer:
   Generics allow you to create reusable code components (functions, classes, or interfaces) that work over a variety of types rather than a single fixed type. They act as type variables—capturing the specific type the user passes in, allowing you to enforce type safety dynamically based on input.

TypeScript
// Generic Function using <T> as a placeholder placeholder type variable
function getFirstElement<T>(arr: T[]): T {
return arr[0];
}

// Code Explanation:
// The type of 'num' is automatically inferred as 'number'
const num = getFirstElement([1, 2, 3]);

// The type of 'str' is automatically inferred as 'string'
const str = getFirstElement(["apple", "banana"]);
