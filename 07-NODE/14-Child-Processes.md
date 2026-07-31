# Child Processes

The `child_process` module lets Node spawn and interact with entirely separate OS processes — including running shell commands, other executables, or even other Node scripts as independent processes.

**Four main methods:**

```js
const { exec, execFile, spawn, fork } = require("child_process");

// exec — runs a shell command, buffers the ENTIRE output in memory, callback-based
exec("ls -la", (err, stdout, stderr) => {
  if (err) return console.error(err);
  console.log(stdout);
});

// spawn — runs a command, streams stdout/stderr in chunks (better for large output / long-running processes)
const child = spawn("ping", ["-c", "4", "google.com"]);
child.stdout.on("data", (data) => console.log(`Output: ${data}`));
child.stderr.on("data", (data) => console.error(`Error: ${data}`));
child.on("close", (code) => console.log(`Process exited with code ${code}`));

// execFile — like exec, but runs an executable directly (not via a shell) — slightly safer/faster
execFile("node", ["--version"], (err, stdout) => console.log(stdout));

// fork — special case of spawn specifically for running ANOTHER NODE.JS script,
// with a built-in IPC channel for message passing (similar to Cluster workers)
const worker = fork("./worker-script.js");
worker.send({ task: "process-data" });
worker.on("message", (result) => console.log("From child:", result));
```

**exec vs spawn — key tradeoff:**

|                 | exec                                               | spawn                                                                             |
| --------------- | -------------------------------------------------- | --------------------------------------------------------------------------------- |
| Output handling | buffers ALL output in memory, returns via callback | streams output incrementally                                                      |
| Good for        | short commands with small output                   | long-running processes, large output, real-time data                              |
| Shell           | runs through a shell (supports pipes, `&&`, etc.)  | runs the command directly by default (no shell features unless `{ shell: true }`) |

**Security note:** `exec()` runs through a shell, meaning **unsanitized user input** in the command string can lead to shell injection vulnerabilities.

```js
// ❌ DANGEROUS — if userInput is "; rm -rf /", this executes arbitrary shell commands
exec(`ls ${userInput}`);

// ✅ SAFER — arguments are passed as an array, not interpolated into a shell string
execFile("ls", [userInput]);
```

**Interview note:** `fork()` is really `spawn()` specialized for Node-to-Node communication with a built-in IPC channel — it's what Cluster uses internally to create worker processes. Use `spawn`/`execFile` over `exec` whenever handling untrusted input or large output.
