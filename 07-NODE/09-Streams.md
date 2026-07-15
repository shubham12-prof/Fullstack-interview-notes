─── 3. Data Flow & Concurrency ───
🔹 Streams
Streams read or write data sequentially in chunks rather than loading the entire file into memory, preventing Out-Of-Memory (OOM) crashes.

JavaScript
const fs = require('fs');

// Read a huge file chunk by chunk, piping it straight to a writable output stream
const readStream = fs.createReadStream('large_video.mp4');
const writeStream = fs.createWriteStream('copy_video.mp4');

readStream.pipe(writeStream);

writeStream.on('finish', () => {
console.log('⚡ Huge file copied smoothly with Streams!');
});s
