─── 1. Core Architecture & Runtime Mechanics ───
🔹 Node Architecture
Node.js is a runtime environment that executes JavaScript code outside a web browser. It is built on the Google V8 JavaScript Engine (which compiles JS into machine code) and libuv (a C library that manages asynchronous, non-blocking I/O operations).

Single-Threaded: Node.js runs JavaScript code on a single main thread (the event loop).

Non-Blocking I/O: Heavy tasks (file reading, network requests) are delegated to the operating system kernel or the libuv Thread Pool (which typically has 4 threads by default), keeping the main thread free.
