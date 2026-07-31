# Node Architecture

Node.js runs JavaScript **outside the browser** using Google's V8 engine, extended with a C++ layer (historically via **libuv**) that provides the event loop, async I/O, file system access, networking, and more — capabilities V8 alone doesn't have.

**High-level architecture:**

```
 ┌─────────────────────────────┐
 │        Your JS Code          │
 ├─────────────────────────────┤
 │   Node.js APIs (fs, http,     │  <- JS bindings to C++ internals
 │   Buffer, streams, etc.)       │
 ├─────────────────────────────┤
 │        V8 Engine                │  <- compiles/executes JS
 ├─────────────────────────────┤
 │        libuv                     │  <- event loop, thread pool, async I/O
 ├─────────────────────────────┤
 │  OS (file system, network, ...)   │
 └─────────────────────────────┘
```

**Key characteristics:**

- **Single-threaded JS execution** — one call stack runs your JS code, same as the browser.
- **Non-blocking I/O** — expensive operations (file reads, network calls, DNS lookups) are delegated to the OS or a background **thread pool** (managed by libuv), so the main thread isn't blocked waiting.
- **Event-driven** — completed async operations fire callbacks/events back on the main thread via the event loop.

```js
const fs = require("fs");

console.log("1: Start");
fs.readFile(__filename, () => {
  console.log("3: File read complete"); // runs later, via the event loop
});
console.log("2: End");
// Output: 1: Start, 2: End, 3: File read complete
// readFile doesn't block — Node registers the callback and moves on immediately.
```

**Why this matters for scalability:** a single Node process can handle thousands of concurrent connections without spawning a thread per connection (unlike traditional thread-per-request server models), because most I/O waits happen off the main thread while it stays free to process other work.

**Interview note:** "Is Node.js single-threaded?" — JS execution on the main thread is single-threaded, but Node itself is NOT purely single-threaded under the hood: libuv maintains a thread pool (default size 4) for certain blocking operations (like `fs` calls, some `crypto` functions, DNS lookups), and Worker Threads/Cluster (see their own files) let you use additional threads/processes explicitly.
