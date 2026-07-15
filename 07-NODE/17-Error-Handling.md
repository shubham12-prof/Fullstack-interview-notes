🔹 Error Handling
Uncaught errors can crash your Node.js server. Use proper try-catch patterns, handle rejections, and intercept uncaught crashes gracefully.

JavaScript
// Handle global promise rejections
process.on('unhandledRejection', (reason, promise) => {
console.error('🚨 Unhandled Promise Rejection:', reason);
// Perform cleanup operations, then exit gracefully
});

// Handle synchronous uncaught exceptions
process.on('uncaughtException', (err) => {
console.error(`💥 System Exception: ${err.message}`);
process.exit(1);
});
