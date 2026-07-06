Q1: What are the states of a Promise, and how does the Micro-task Queue prioritize them?
Answer:
A Promise handles an asynchronous operation, existing in one of three states: pending, fulfilled (triggers .then()), or rejected (triggers .catch()).

Promise callbacks are pushed into the specialized Micro-task Queue, which takes priority over the standard macro-task queue (setTimeout).

Critical Rule: The Event Loop will empty the entire Micro-task queue before processing a single macro-task from the main task queue.

JavaScript
console.log("Start");

setTimeout(() => console.log("Timeout (Macro-task)"), 0);
Promise.resolve().then(() => console.log("Promise (Micro-task)"));

console.log("End");

// Code Explanation Execution Order:
// 1. "Start" (Synchronous) -> 2. "End" (Synchronous)
// 3. "Promise" (Micro-task wins) -> 4. "Timeout" (Macro-task runs last)
