🔹 Child Processes
The child_process module allows you to run system terminal commands or native shell scripts directly from within Node.js.

JavaScript
const { exec } = require('child_process');

// Run a terminal command (e.g., list files)
exec('ls -lh', (error, stdout, stderr) => {
if (error) {
console.error(`Exec Error: ${error}`);
return;
}
console.log(`📂 Current Directory Files:\n${stdout}`);
});
