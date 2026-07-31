# Coding Challenges

### 1. Build a simple HTTP server with basic routing (no framework)

```js
const http = require("http");
const url = require("url");

const server = http.createServer((req, res) => {
  const { pathname } = url.parse(req.url);
  res.setHeader("Content-Type", "application/json");

  if (pathname === "/health" && req.method === "GET") {
    res.writeHead(200);
    res.end(JSON.stringify({ status: "ok" }));
  } else {
    res.writeHead(404);
    res.end(JSON.stringify({ error: "Not Found" }));
  }
});

server.listen(3000);
```

### 2. Implement a custom EventEmitter from scratch

```js
class MyEmitter {
  constructor() {
    this.events = {};
  }
  on(event, listener) {
    (this.events[event] ??= []).push(listener);
    return this;
  }
  emit(event, ...args) {
    (this.events[event] || []).forEach((listener) => listener(...args));
    return this.events[event]?.length > 0;
  }
  off(event, listener) {
    this.events[event] = (this.events[event] || []).filter(
      (l) => l !== listener,
    );
    return this;
  }
}
```

### 3. Read a large file and count the number of lines, using streams (memory-efficient)

```js
const fs = require("fs");
const readline = require("readline");

async function countLines(filePath) {
  const rl = readline.createInterface({ input: fs.createReadStream(filePath) });
  let count = 0;
  for await (const _line of rl) count++;
  return count;
}
```

### 4. Promisify a callback-based function

```js
function readFileCb(path, callback) {
  require("fs").readFile(path, "utf8", callback);
}

function promisify(fn) {
  return (...args) =>
    new Promise((resolve, reject) => {
      fn(...args, (err, result) => (err ? reject(err) : resolve(result)));
    });
}

const readFileAsync = promisify(readFileCb);
// Node also ships this exact utility: require('util').promisify
```

### 5. Implement a simple rate limiter middleware (token bucket, in-memory)

```js
function rateLimiter({ windowMs, max }) {
  const hits = new Map(); // ip -> { count, resetAt }
  return (req, res, next) => {
    const ip = req.socket.remoteAddress;
    const now = Date.now();
    const entry = hits.get(ip);

    if (!entry || now > entry.resetAt) {
      hits.set(ip, { count: 1, resetAt: now + windowMs });
      return next();
    }
    if (entry.count >= max) {
      return res.status(429).json({ error: "Too many requests" });
    }
    entry.count++;
    next();
  };
}
```

### 6. Recursively find all files with a given extension in a directory (async)

```js
const fs = require("fs/promises");
const path = require("path");

async function findFiles(dir, ext) {
  const entries = await fs.readdir(dir, { withFileTypes: true });
  const results = [];
  for (const entry of entries) {
    const fullPath = path.join(dir, entry.name);
    if (entry.isDirectory()) {
      results.push(...(await findFiles(fullPath, ext)));
    } else if (entry.name.endsWith(ext)) {
      results.push(fullPath);
    }
  }
  return results;
}
```

### 7. Run a CPU-intensive task in a Worker Thread and return the result via a Promise

```js
const { Worker } = require("worker_threads");

function runWorker(workerData) {
  return new Promise((resolve, reject) => {
    const worker = new Worker("./task.js", { workerData });
    worker.on("message", resolve);
    worker.on("error", reject);
    worker.on("exit", (code) => {
      if (code !== 0)
        reject(new Error(`Worker stopped with exit code ${code}`));
    });
  });
}
```
