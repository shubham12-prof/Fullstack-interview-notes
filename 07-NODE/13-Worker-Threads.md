🔹 Worker Threads
Worker Threads run CPU-heavy tasks on separate threads without blocking the main event loop. Unlike child processes, worker threads can share memory safely.

JavaScript
const { Worker, isMainThread, parentPort, workerData } = require('worker_threads');

if (isMainThread) {
// Main thread: Start a background worker to calculate heavy math
const worker = new Worker(\_\_filename, { workerData: 40 });

worker.on('message', (result) => {
console.log(`🎯 Heavy Fibonacci result received: ${result}`);
});
} else {
// Worker Thread: Execute complex calculations
const num = workerData;
const fib = (n) => (n < 2 ? n : fib(n - 1) + fib(n - 2));

parentPort.postMessage(fib(num));
}
