# Event Loop

The mechanism that lets Node.js perform non-blocking I/O despite JS being single-threaded — it continuously checks for completed async work and executes the associated callbacks, cycling through a fixed set of **phases**.

**The six phases (each phase has its own callback queue):**

```
   ┌───────────────────────────┐
┌─>│           timers            │  <- setTimeout, setInterval callbacks
│  ├───────────────────────────┤
│  │     pending callbacks        │  <- deferred I/O callbacks from previous cycle
│  ├───────────────────────────┤
│  │       idle, prepare           │  <- internal use only
│  ├───────────────────────────┤
│  │           poll                 │  <- fetch new I/O events; executes I/O callbacks
│  ├───────────────────────────┤
│  │          check                  │  <- setImmediate() callbacks
│  ├───────────────────────────┤
│  │      close callbacks              │  <- e.g. socket.on('close', ...)
│  └───────────────────────────┘
```

Between EVERY phase transition (and after each callback), Node drains the **microtask queues** first: `process.nextTick()` callbacks (highest priority, before Promise microtasks), then Promise `.then/.catch/.finally` callbacks.

```js
console.log("1: sync");

setTimeout(() => console.log("5: setTimeout"), 0); // timers phase
setImmediate(() => console.log("4: setImmediate")); // check phase
process.nextTick(() => console.log("2: nextTick")); // microtask, highest priority
Promise.resolve().then(() => console.log("3: promise")); // microtask

console.log("1.5: sync end");
// Output: 1: sync, 1.5: sync end, 2: nextTick, 3: promise, then 4/5
// (order between setTimeout(,0) and setImmediate is not deterministic at the top level,
//  but INSIDE an I/O callback, setImmediate always fires before setTimeout)
```

```js
const fs = require("fs");
fs.readFile(__filename, () => {
  setTimeout(() => console.log("timeout"), 0);
  setImmediate(() => console.log("immediate")); // always logs BEFORE timeout here,
}); // since we're already in the poll phase,
// and check comes right after poll
```

**Interview note:** `process.nextTick()` callbacks run before Promise microtasks and before moving to the next event loop phase — overusing `process.nextTick()` recursively can starve the event loop, preventing I/O from ever being processed ("I/O starvation").
