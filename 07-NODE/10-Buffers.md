# Buffers

A `Buffer` is a fixed-size chunk of raw binary data (a lot like a byte array), used because JS strings weren't originally designed to handle binary data efficiently. Buffers are what streams actually pass around under the hood when working with files, network sockets, or any binary data.

```js
// Creating buffers
const buf1 = Buffer.from("Hello", "utf8"); // from a string
const buf2 = Buffer.alloc(10); // 10 zero-filled bytes
const buf3 = Buffer.allocUnsafe(10); // 10 uninitialized bytes (faster, but may contain old memory data — must be filled before use)

// Reading/writing
buf1.toString("utf8"); // "Hello" — convert back to string
buf1[0]; // 72 — raw byte value (charcode of 'H')
buf1.length; // 5 — byte length (not always same as string.length for multi-byte chars!)

// Concatenating
const combined = Buffer.concat([buf1, Buffer.from(" World")]);
combined.toString(); // "Hello World"

// Slicing (returns a VIEW into the same underlying memory, not a copy)
const slice = buf1.slice(0, 2);
slice.toString(); // "He"
```

**Common use case — handling binary/streamed data:**

```js
const fs = require("fs");
fs.readFile("image.png", (err, buffer) => {
  console.log(buffer.length); // file size in bytes
  console.log(Buffer.isBuffer(buffer)); // true — readFile returns a Buffer by default
});

// Streams emit Buffer chunks by default (unless an encoding is specified)
req.on("data", (chunk) => {
  console.log(Buffer.isBuffer(chunk)); // true
});
```

**Interview note:** `Buffer.from(str).length` may NOT equal `str.length` for non-ASCII text, because `.length` on a string counts UTF-16 code units, while `Buffer.length` counts raw bytes (a single emoji or accented character can take multiple bytes in UTF-8). This mismatch is a classic gotcha when slicing multi-byte strings by byte length.
