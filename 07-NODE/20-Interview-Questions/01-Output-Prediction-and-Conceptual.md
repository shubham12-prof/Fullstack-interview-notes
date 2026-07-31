# Output Prediction & Conceptual Questions

## Output-Prediction Questions

**Q1.**

```js
console.log("1");
setTimeout(() => console.log("2"), 0);
Promise.resolve().then(() => console.log("3"));
process.nextTick(() => console.log("4"));
console.log("5");
```

<details><summary>Answer</summary>

`1, 5, 4, 3, 2` — synchronous code runs first (1, 5), then `process.nextTick` (highest-priority microtask), then Promise microtasks, then macrotasks (`setTimeout`, in the timers phase).

</details>

**Q2.**

```js
const fs = require("fs");
console.log("start");
fs.readFile(__filename, () => console.log("file read"));
console.log("end");
```

<details><summary>Answer</summary>

`start, end, file read` — `fs.readFile` is non-blocking; its callback runs later via the event loop (poll phase) once the OS/thread pool completes the read.

</details>

**Q3.**

```js
const EventEmitter = require("events");
const emitter = new EventEmitter();
emitter.emit("greet", "hello"); // emitted BEFORE the listener is registered
emitter.on("greet", (msg) => console.log(msg));
```

<details><summary>Answer</summary>

Nothing is logged — `emit()` only calls listeners registered AT THE TIME it runs. Since `.on()` was called after `.emit()`, there was no listener yet to catch it.

</details>

**Q4.**

```js
console.log(require.cache[require.resolve("./counter")] !== undefined);
require("./counter");
console.log(require.cache[require.resolve("./counter")] !== undefined);
```

<details><summary>Answer</summary>

`false`, then `true` — before the first `require("./counter")` call anywhere, the module isn't cached; after requiring it once, Node caches the module (`module.exports`), so subsequent requires return the same cached instance.

</details>

---

## Conceptual Questions

1. Why is Node.js described as "single-threaded" even though it uses a thread pool internally?
2. What's the difference between `process.nextTick()` and `setImmediate()`?
3. Explain the difference between `spawn`, `exec`, `execFile`, and `fork` in `child_process`.
4. When would you choose Worker Threads over Cluster (or vice versa)?
5. What is backpressure in Node streams, and why does it matter?
6. Why should you avoid synchronous `fs` methods (like `readFileSync`) in a request handler?
7. How does CommonJS module caching work, and what's a practical implication of it?
8. What's the difference between `npm install` and `npm ci`, and when should each be used?
9. Why is it dangerous to use `exec()` with unsanitized user input?
10. What's the recommended way to handle an `uncaughtException` in a production Node app, and why?
