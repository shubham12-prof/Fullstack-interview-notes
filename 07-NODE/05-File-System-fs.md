🔹 File System (fs)
Provides APIs for interacting with the file system. Use the modern Promises API to avoid blocking the main thread or writing nesting-heavy callbacks.

JavaScript
const fs = require('fs/promises');

async function handleFile() {
try {
// Write data to a file
await fs.writeFile('notes.txt', 'Hello Node.js Developer!');
console.log('📝 File written successfully.');

    // Read data from file
    const content = await fs.readFile('notes.txt', 'utf-8');
    console.log(`📖 File contents: ${content}`);

} catch (err) {
console.error('❌ File Error:', err);
}
}
handleFile();
