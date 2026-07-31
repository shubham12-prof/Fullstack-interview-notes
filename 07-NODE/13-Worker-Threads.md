# Worker Threads

A module for running JS in parallel **threads** within the same process — unlike Cluster (separate processes), Worker Threads can share memory (via `SharedArrayBuffer`) and are lighter-weight, making them well suited to CPU-intensive computation that would otherwise block the main event loop.

```js
// main.js
const { Worker } = require("worker_threads");

const worker = new Worker("./heavy-task.js", {
  workerData: { number: 45 }, // data passed to the worker on creation
});

worker.on("message", (result) => {
  console.log("Result from worker:", result);
});
worker.on("error", (err) => console.error(err));
worker.on("exit", (code) => console.log(`Worker exited with code ${code}`));
```

```js
// heavy-task.js
const { parentPort, workerData } = require("worker_threads");

function fibonacci(n) {
  return n <= 1 ? n : fibonacci(n - 1) + fibonacci(n - 2); // CPU-intensive, blocking work
}

const result = fibonacci(workerData.number);
parentPort.postMessage(result); // send result back to the main thread
```

**Why not just do this on the main thread?**

```js
// ❌ Blocks the event loop — the entire server becomes unresponsive during this calculation
app.get("/fib/:n", (req, res) => {
  res.json({ result: fibonacci(req.params.n) });
});

// ✅ Offload to a worker thread — main thread (and event loop) stays responsive
app.get("/fib/:n", (req, res) => {
  const worker = new Worker("./heavy-task.js", {
    workerData: { number: req.params.n },
  });
  worker.on("message", (result) => res.json({ result }));
});
```

**Cluster vs Worker Threads:**

|                | Cluster                                     | Worker Threads                               |
| -------------- | ------------------------------------------- | -------------------------------------------- |
| Isolation      | separate OS processes                       | separate threads, same process               |
| Memory sharing | none (IPC only)                             | possible, via SharedArrayBuffer              |
| Overhead       | higher (full process per worker)            | lower                                        |
| Best for       | scaling stateless HTTP servers across cores | offloading CPU-heavy synchronous computation |

**Interview note:** Worker Threads solve a different problem than async I/O — async I/O (Promises, callbacks) doesn't block the event loop because the OS handles the waiting, but pure **CPU-bound** synchronous work (heavy computation, image processing, encryption) DOES block the event loop no matter how it's written, and needs to be offloaded to a Worker Thread (or a separate process) to keep the server responsive.
