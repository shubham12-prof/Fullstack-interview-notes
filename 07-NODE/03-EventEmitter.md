🔹 EventEmitter
Node.js is heavily event-driven. The EventEmitter class allows you to create, listen to, and trigger custom events.

JavaScript
const EventEmitter = require('events');

// Create a custom emitter class
class UserActivity extends EventEmitter {}
const userActivity = new UserActivity();

// 1. Register a listener
userActivity.on('login', (username, timestamp) => {
console.log(`🔑 Event Logged: ${username} logged in at ${timestamp}`);
});

// 2. Trigger (emit) the event
userActivity.emit('login', 'Alice', new Date().toLocaleTimeString());
