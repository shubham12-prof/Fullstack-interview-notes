# File System (fs)

The built-in module for interacting with the file system — reading, writing, updating, deleting files and directories. Offers three API styles: callback-based, Promise-based (`fs/promises`), and synchronous.

```js
const fs = require("fs");
const fsPromises = require("fs/promises");

// Callback style (traditional, non-blocking)
fs.readFile("data.txt", "utf8", (err, data) => {
  if (err) return console.error(err);
  console.log(data);
});

// Promise style (modern, non-blocking) — preferred for async/await code
async function readData() {
  try {
    const data = await fsPromises.readFile("data.txt", "utf8");
    console.log(data);
  } catch (err) {
    console.error(err);
  }
}

// Synchronous style — BLOCKS the event loop until done; use sparingly
const data = fs.readFileSync("data.txt", "utf8");
```

**Common operations:**

```js
await fsPromises.writeFile("out.txt", "Hello, World!"); // overwrite/create
await fsPromises.appendFile("log.txt", "New line\n"); // append
await fsPromises.mkdir("newDir", { recursive: true }); // create nested dirs
await fsPromises.readdir("someDir"); // list directory contents
await fsPromises.stat("data.txt"); // file metadata (size, mtime, isFile())
await fsPromises.unlink("data.txt"); // delete a file
await fsPromises.rm("someDir", { recursive: true, force: true }); // delete a directory
await fsPromises.rename("old.txt", "new.txt");
await fsPromises.copyFile("a.txt", "b.txt");
```

**Watching for changes:**

```js
fs.watch("data.txt", (eventType, filename) => {
  console.log(`${filename} changed: ${eventType}`);
});
```

**Interview note:** never use the synchronous `fs.*Sync` methods in the main request-handling path of a server — they block the entire event loop, freezing every other in-flight request until the operation completes. Sync methods are only acceptable for one-off scripts or startup-time config loading, not per-request logic.
