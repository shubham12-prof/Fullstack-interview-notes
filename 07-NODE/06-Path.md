🔹 Path
Safely resolves file and directory paths across different Operating Systems (which use different path separators: / on Unix vs \ on Windows).

JavaScript
const path = require('path');

// Join directories securely
const absolutePath = path.join(\_\_dirname, 'src', 'config', 'db.js');
console.log('📂 Combined Path:', absolutePath);

// Extract path properties
console.log('📄 File Extension:', path.extname(absolutePath)); // '.js'
console.log('🏷️ File Name:', path.basename(absolutePath)); // 'db.js'
