🔹 Event Loop
The Event Loop is the heart of Node.js. It allows Node.js to perform non-blocking I/O operations by offloading tasks to the system kernel whenever possible.

The loop operates in 6 main phases, running in a continuous cycle:

Poll: Retrieves new I/O events; executes I/O related callbacks.

Check: Executes callbacks registered via setImmediate().

Close Callbacks: Executes close callbacks, e.g., socket.on('close', ...).

Timers: Executes callbacks scheduled by setTimeout() and setInterval().

Pending Callbacks: Executes I/O callbacks deferred to the next loop iteration.

Idle, Prepare: Used internally by Node.js.

⚠️ Crucial Note: process.nextTick() and Promise microtasks are executed immediately after the current phase completes, before moving to the next phase.

JavaScript
setTimeout(() => console.log('🕐 Timer (setTimeout)'), 0);
setImmediate(() => console.log('🔄 Check (setImmediate)'));
process.nextTick(() => console.log('⚡ Urgent (process.nextTick)'));
Promise.resolve().then(() => console.log('🔬 Promise Microtask'));

console.log('🏁 Start');

// --- Execution Output Order: ---
// 1. 🏁 Start (Synchronous code runs first)
// 2. ⚡ Urgent (nextTick queue processed immediately after current script)
// 3. 🔬 Promise Microtask (Microtasks follow nextTick)
// 4. 🕐 Timer (Runs during Timers phase)
// 5. 🔄 Check (Runs during Check phase)
