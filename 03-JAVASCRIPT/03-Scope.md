Q1: How does Scope and the Scope Chain work in JavaScript?
Answer:
Scope determines the accessibility of variables. JavaScript uses Lexical Scoping, meaning variable access is locked in place when functions are written, not when they are executed.

When a variable is accessed, the engine looks inside the immediate local scope. If it cannot find it, it follows the Scope Chain upward into outer parent environments until it hits the Global Scope. If it still can't find it, it returns a ReferenceError.

JavaScript
const globalVar = "global";

function outer() {
const outerVar = "outer";

function inner() {
const innerVar = "inner";
// Code Explanation:
// This inner function has access to all variables along the scope chain line
console.log(innerVar, outerVar, globalVar);
}
inner();
}
outer();
