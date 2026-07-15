🔹 HTTP Module
Allows Node.js to act as a web server without any external framework like Express.

JavaScript
const http = require('http');

const server = http.createServer((req, res) => {
if (req.url === '/' && req.method === 'GET') {
res.writeHead(200, { 'Content-Type': 'application/json' });
res.end(JSON.stringify({ message: 'Welcome to Node.js HTTP Server' }));
} else {
res.writeHead(404, { 'Content-Type': 'text/plain' });
res.end('Not Found');
}
});

server.listen(3000, () => {
console.log('🚀 Server listening on http://localhost:3000');
});
