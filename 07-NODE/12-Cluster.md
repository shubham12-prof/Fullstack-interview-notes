# Cluster

Node's built-in module for spawning multiple **processes** (workers), each with its own event loop and memory, letting a Node app take advantage of multi-core CPUs — since a single Node process only uses one core for JS execution by default.

```js
const cluster = require("cluster");
const http = require("http");
const os = require("os");

if (cluster.isPrimary) {
  const numCPUs = os.cpus().length;
  console.log(`Primary ${process.pid} is running, forking ${numCPUs} workers`);

  for (let i = 0; i < numCPUs; i++) {
    cluster.fork(); // each fork is a full new Node process running this same file
  }

  cluster.on("exit", (worker, code, signal) => {
    console.log(`Worker ${worker.process.pid} died, restarting...`);
    cluster.fork(); // restart a crashed worker — improves resilience
  });
} else {
  // Worker processes share the SAME server port — the OS/Node load-balances connections across them
  http
    .createServer((req, res) => {
      res.end(`Handled by worker ${process.pid}`);
    })
    .listen(3000);

  console.log(`Worker ${process.pid} started`);
}
```

**Key characteristics:**

- Each worker is a **separate OS process** with its own memory — no shared memory/variables between workers (unlike threads).
- Workers communicate with the primary process via IPC (`worker.send()` / `process.on('message', ...)`) if needed.
- The primary process distributes incoming connections across workers (round-robin by default on most platforms).

```js
// IPC between primary and worker
if (cluster.isPrimary) {
  const worker = cluster.fork();
  worker.send({ type: "greeting", data: "Hello worker" });
  worker.on("message", (msg) => console.log("From worker:", msg));
} else {
  process.on("message", (msg) => {
    process.send({ type: "reply", data: "Hello primary" });
  });
}
```

**Interview note:** Cluster is typically used to scale a **stateless HTTP server** across CPU cores in production (often in combination with, or replaced by, a process manager like PM2's cluster mode). Since each worker has separate memory, any shared state (sessions, caches) needs an external store (Redis, a database) rather than in-process variables.
