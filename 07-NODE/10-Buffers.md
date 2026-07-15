🔹 Buffers
Buffers are temporary raw memory spaces allocated outside the V8 heap, used to handle binary data sequences.

JavaScript
// Create a buffer from a string
const buf = Buffer.from('Hello 🟢', 'utf-8');

console.log('Binary Hex Data:', buf);
console.log('Length in Bytes:', buf.length); // 10 bytes (emoji takes 4 bytes)
console.log('Decoded String:', buf.toString('utf-8'));
