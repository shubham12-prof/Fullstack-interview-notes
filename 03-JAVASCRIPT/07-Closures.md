Q1: What is a Closure, and can you provide a practical use-case?
Answer:
A closure is formed when a nested inner function retains access to variables from its outer parent scope, even after the parent function has finished executing and closed its own execution context.

JavaScript
function createCounter() {
let count = 0; // Private variable trapped inside the closure scope

return {
increment: function() {
count++;
return count;
}
};
}

// Code Explanation:
const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.count); // undefined (safely hidden from external modification!
