Q1: Why is async/await generally preferred over raw Promises?
Answer:
async/await is a clean syntactic wrapper built directly on top of native Promises. It allows asynchronous code to be written and read like standard, step-by-step synchronous code. This eliminates deeply nested .then() chains ("callback hell") and maps error handling directly to traditional try/catch blocks.
