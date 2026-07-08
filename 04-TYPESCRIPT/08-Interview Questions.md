7. Interview Questions Wrap-Up
   Q1: What is Type Assertion (Type Casting) in TypeScript, and when should you use as vs. <type>?
   Answer:
   Type assertion tells the TypeScript compiler: "Trust me, I know what I'm doing; I know the type of this object better than you do." It doesn't perform any actual runtime checking or transformation.

Modern standards strongly recommend using the as NewType syntax over the older <NewType> angle-bracket syntax, because angle-brackets conflict directly with JSX syntax markers inside React projects (.tsx).

TypeScript
// Using 'as' for Type Assertion
const canvasElement = document.getElementById("main-canvas") as HTMLCanvasElement;

// Code Explanation:
// By default, getElementById returns 'HTMLElement | null'.
// Asserting 'as HTMLCanvasElement' tells the compiler it can safely access specific methods like .getContext().
const ctx = canvasElement.getContext("2d");
