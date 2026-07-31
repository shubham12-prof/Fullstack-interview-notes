# Process

`process` is a global object available in every Node module, providing information about, and control over, the currently running Node.js process.

```js
process.argv; // array of command-line arguments (argv[0]=node path, argv[1]=script path, argv[2+]=user args)
process.env; // environment variables (see the Environment Variables file)
process.platform; // 'linux', 'darwin', 'win32'
process.version; // Node.js version, e.g. 'v20.11.0'
process.pid; // current process ID
process.cwd(); // current working directory

process.exit(0); // exit immediately with a success code (0 = success, non-zero = failure)
process.exit(1);
```

**Standard streams:**

```js
process.stdout.write("Hello\n"); // like console.log, but without the trailing newline auto-added
process.stderr.write("Error!\n");
```

**Handling process-level events:**

```js
process.on("exit", (code) => {
  console.log(`Process exiting with code ${code}`); // only sync cleanup allowed here
});

process.on("uncaughtException", (err) => {
  console.error("Uncaught exception:", err);
  process.exit(1); // best practice: exit after an uncaught exception, don't try to "recover"
});

process.on("unhandledRejection", (reason) => {
  console.error("Unhandled promise rejection:", reason);
});

// Graceful shutdown on termination signals (e.g. from Docker/Kubernetes/Ctrl+C)
process.on("SIGTERM", () => {
  console.log("Received SIGTERM, shutting down gracefully");
  server.close(() => process.exit(0));
});
process.on("SIGINT", () => {
  /* Ctrl+C */
});
```

**`process.nextTick()` vs `setImmediate()`:**

```js
process.nextTick(() => console.log("nextTick")); // runs BEFORE the event loop continues to the next phase
setImmediate(() => console.log("immediate")); // runs in the 'check' phase, after I/O callbacks
```

**Interview note:** after an `uncaughtException`, the process is in an undefined/potentially corrupted state — best practice is to log it, perform minimal cleanup, and exit (`process.exit(1)`), letting a process manager (PM2, Kubernetes) restart it, rather than trying to keep running.
