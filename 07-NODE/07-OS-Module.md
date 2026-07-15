🔹 OS Module
Provides information about the host machine's operating system.

JavaScript
const os = require('os');

console.log('💻 Operating System:', os.type());
console.log('⚙️ CPU Architecture:', os.arch());
console.log('🔋 Free Memory:', (os.freemem() / (1024 \*\* 3)).toFixed(2), 'GB');
console.log('📡 Network Interfaces:', Object.keys(os.networkInterfaces()));
