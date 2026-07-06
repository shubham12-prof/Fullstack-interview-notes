Q1: What is Hoisting and the Temporal Dead Zone (TDZ)?
Answer:

Hoisting: During the compilation phase, the JavaScript engine moves declarations (variables and functions) to the top of their enclosing scope. Functions are fully hoisted, while var variables are hoisted and initialized as undefined.

Temporal Dead Zone (TDZ): let and const variables are hoisted but not initialized. The TDZ is the region of code stretching from the start of the block block until the exact line where the variable is explicitly declared. Accessing them inside this zone throws a ReferenceError.

JavaScript
console.log(myVar); // Outputs: undefined (hoisted and initialized)
var myVar = 5;

// Code Explanation:
// The browser knows 'myLet' exists, but it sits in the TDZ until line 9 runs
console.log(myLet); // Throws ReferenceError: Cannot access 'myLet' before initialization
let myLet = 10;
