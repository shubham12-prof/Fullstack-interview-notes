🔹 Process
The process object provides control over the current running Node.js process.

JavaScript
// Access system configurations and runtime paths
console.log('Platform:', process.platform);
console.log('Node Version:', process.version);

// Exit a process programmatically (0 indicates successful completion)
if (process.argv.includes('--halt')) {
console.log('Aborting process...');
process.exit(1); // 1 indicates execution error
}
