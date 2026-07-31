# Streams

An abstraction for working with data that's read/written **incrementally, in chunks**, rather than loading the entire thing into memory at once — essential for large files, network data, and anything where memory efficiency matters.

**Four types of streams:**

| Type      | Purpose                                               | Examples                                       |
| --------- | ----------------------------------------------------- | ---------------------------------------------- |
| Readable  | source you read data FROM                             | `fs.createReadStream`, incoming HTTP request   |
| Writable  | destination you write data TO                         | `fs.createWriteStream`, outgoing HTTP response |
| Duplex    | both readable AND writable                            | TCP sockets                                    |
| Transform | duplex stream that modifies data as it passes through | `zlib` gzip/gunzip, encryption streams         |

```js
const fs = require("fs");

// Readable stream — reads a large file in chunks, not all at once
const readStream = fs.createReadStream("bigfile.txt", { encoding: "utf8" });
readStream.on("data", (chunk) => console.log("Received chunk:", chunk.length));
readStream.on("end", () => console.log("Done reading"));
readStream.on("error", (err) => console.error(err));

// Writable stream
const writeStream = fs.createWriteStream("output.txt");
writeStream.write("Hello, ");
writeStream.write("World!");
writeStream.end();
```

**`.pipe()` — connects a readable stream directly to a writable one, handling backpressure automatically:**

```js
const readStream = fs.createReadStream("input.txt");
const writeStream = fs.createWriteStream("output.txt");
readStream.pipe(writeStream); // efficiently streams data without loading it all into memory

// Chaining transforms — e.g., gzip compression while copying a file
const zlib = require("zlib");
fs.createReadStream("input.txt")
  .pipe(zlib.createGzip())
  .pipe(fs.createWriteStream("input.txt.gz"));
```

**Why streams matter — memory comparison:**

```js
// ❌ Loads the ENTIRE file into memory — can crash on very large files
const data = fs.readFileSync("huge-file.txt");
res.end(data);

// ✅ Streams the file in small chunks, constant memory usage regardless of file size
fs.createReadStream("huge-file.txt").pipe(res);
```

**Backpressure:** when a writable stream can't keep up with incoming data (e.g., slow disk/network), it signals the readable stream to pause — `.pipe()` handles this automatically; manual stream handling requires checking the return value of `.write()` and listening for `'drain'`.

**Interview note:** "Why use streams instead of just reading the whole file?" — Streams keep memory usage constant regardless of input size, and let you start processing/sending data before the entire source is even available (lower latency, e.g., video streaming or large API responses).
