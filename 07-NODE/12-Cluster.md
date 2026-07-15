🔹 Cluster
The cluster module lets you spawn multiple instances of your application (one for each CPU core). These instances run on their own threads and share the same server port, helping to load-balance high traffic.

JavaScript
const cluster = require('cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isPrimary) {
console.log(`👑 Primary controller process ${process.pid} is running.`);

// Fork worker threads based on CPU cores
for (let i = 0; i < numCPUs; i++) {
cluster.fork();
}

cluster.on('exit', (worker) => {
console.log(`⚠️ Worker process ${worker.process.pid} died. Spawning replacement...`);
cluster.fork();
});
} else {
// Workers share the TCP port 8000
http.createServer((req, res) => {
res.writeHead(200);
res.end(`Handled by Worker Process: ${process.pid}\n`);
}).listen(8000);

console.log(`👷 Worker process ${process.pid} spawned.`);
}
