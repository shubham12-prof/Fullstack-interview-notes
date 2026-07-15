─── 5. Top Tech Node.js Interview Questions ───
Q1: What is the difference between Worker Threads and Clusters?
Clusters: Launch multiple complete instances of your Node.js application, each running in its own separate process with its own memory space. It is designed to scale network-heavy HTTP applications.

Worker Threads: Run inside a single main process, sharing the same memory space. They are designed to handle CPU-heavy mathematical operations without blocking the main event loop.

Q2: What is "Backpressure" in Node.js Streams?
Backpressure occurs when the writable stream cannot write data as fast as the readable stream is reading it. This causes data chunks to queue up in system memory, which can crash the application.

The Solution: The .pipe() method handles backpressure automatically by pausing the readable stream until the writable stream is ready to receive more data.

Q3: Why is Node.js called single-threaded if it uses a Thread Pool?
Your JavaScript code runs strictly on one single thread (the Event Loop thread). However, tasks like file operations (fs), cryptography (crypto), and compression (zlib) are asynchronous and expensive. Node offloads these tasks to the background libuv thread pool. Once those threads finish the work, they send the results back to the main thread to execute your JavaScript callback.

Q4: What is the difference between setImmediate() and setTimeout(fn, 0)?
setTimeout(fn, 0) schedules execution during the Timers phase of the Event Loop.

setImmediate(fn) schedules execution during the Check phase of the Event Loop.

If called within an I/O cycle (like inside a file read callback), setImmediate is guaranteed to run before setTimeout, regardless of current processor speed.
