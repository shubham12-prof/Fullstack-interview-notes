# Error Handling

Node error handling spans several layers — synchronous try/catch, callback-style error-first conventions, Promise rejections, and process-level safety nets.

**Callback convention — "error-first" callbacks:**

```js
fs.readFile("file.txt", (err, data) => {
  if (err) return console.error("Error:", err.message); // ALWAYS check err first
  console.log(data);
});
```

**Async/await with try/catch (preferred in modern code):**

```js
async function readConfig() {
  try {
    const data = await fs.promises.readFile("config.json", "utf8");
    return JSON.parse(data);
  } catch (err) {
    console.error("Failed to read config:", err.message);
    throw err; // re-throw if the caller needs to know, or handle here if recoverable
  }
}
```

**Custom error classes (same pattern as browser JS):**

```js
class NotFoundError extends Error {
  constructor(resource) {
    super(`${resource} not found`);
    this.name = "NotFoundError";
    this.statusCode = 404;
  }
}

class ValidationError extends Error {
  constructor(message, field) {
    super(message);
    this.name = "ValidationError";
    this.statusCode = 400;
    this.field = field;
  }
}
```

**Centralized error-handling middleware (Express example):**

```js
app.use((err, req, res, next) => {
  const statusCode = err.statusCode || 500;
  console.error(err); // log full error server-side
  res.status(statusCode).json({
    error: err.message,
    ...(process.env.NODE_ENV !== "production" && { stack: err.stack }), // hide stack traces in prod
  });
});
```

**Process-level safety nets (last resort, not a substitute for proper handling):**

```js
process.on("uncaughtException", (err) => {
  console.error("Uncaught exception:", err);
  process.exit(1); // don't try to keep running — process state may be corrupted
});
process.on("unhandledRejection", (reason) => {
  console.error("Unhandled rejection:", reason);
  process.exit(1);
});
```

**Interview note:** "Why exit the process after an uncaught exception instead of just logging it?" — once an exception escapes all handlers, the process may be in an inconsistent state (partially completed operations, corrupted in-memory data); best practice is to log, exit, and let a process manager (PM2, Docker, Kubernetes) restart a clean instance, rather than risk running in a broken state.
