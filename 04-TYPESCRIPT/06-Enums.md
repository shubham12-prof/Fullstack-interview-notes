5. Enums
   Q1: What are Enums, and what is the difference between a standard Enum and a const enum?
   Answer:
   Enums allow developers to define a set of named constants, making code more readable by replacing magic strings or numbers.

Standard Enum: Compiles into a real, JavaScript lookup object in your final build file. This supports reverse mapping (getting the enum key from the value) but adds slight runtime overhead.

const enum: Completely erased during compilation. The compiler strips the enum definition away and directly inlines the raw scalar values wherever they are used, saving file size and optimization steps.

TypeScript
// Standard Enum
enum StatusCodes {
Success = 200,
NotFound = 404
}

// const enum
const enum Direction {
Up,
Down
}

// Code Explanation:
// During compilation, the line below transforms into raw, minimal JavaScript:
// const move = 0 /_ Up _/;
const move = Direction.Up;
