# OS Module

The built-in module for retrieving operating-system-level information — CPU, memory, network interfaces, user info, platform details.

```js
const os = require("os");

os.platform(); // 'linux', 'darwin', 'win32'
os.arch(); // 'x64', 'arm64'
os.type(); // 'Linux', 'Darwin', 'Windows_NT'
os.release(); // OS version string

os.cpus(); // array of CPU core info (model, speed, times)
os.cpus().length; // number of logical CPU cores — often used to size a Cluster/thread pool

os.totalmem(); // total system RAM, in bytes
os.freemem(); // available RAM, in bytes

os.homedir(); // current user's home directory
os.tmpdir(); // system's temp directory path
os.hostname(); // machine's hostname

os.networkInterfaces(); // network interface details (IP addresses, etc.)
os.uptime(); // system uptime, in seconds
os.userInfo(); // { username, homedir, shell, uid, gid }
```

**Practical example — sizing a worker pool to available CPUs:**

```js
const numCPUs = os.cpus().length;
console.log(`Spinning up ${numCPUs} worker processes`);
// commonly used alongside the Cluster module to fork one worker per core
```

**Interview note:** the OS module is mostly used for environment introspection (e.g., deciding cluster/worker pool size, logging system diagnostics) rather than for direct application logic — it doesn't let you control the OS, only read information from it.
