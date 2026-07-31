# CommonJS

Node's original, default module system — synchronous, uses `require()` to import and `module.exports`/`exports` to export.

```js
// math.js
function add(a, b) {
  return a + b;
}
const PI = 3.14159;

module.exports = { add, PI };
// or individually: exports.add = add;

// main.js
const { add, PI } = require("./math");
console.log(add(2, 3)); // 5
```

**How `require()` works internally:**

1. Resolves the module path (relative file, `node_modules` package, or built-in module).
2. If already cached (in `require.cache`), returns the cached `module.exports` immediately.
3. Otherwise, wraps the file's code in a function, executes it synchronously, and caches the result.

```js
// Node wraps every CommonJS module roughly like this before executing it:
(function (exports, require, module, __filename, __dirname) {
  // your module code here
});
```

This wrapper is why `__filename`, `__dirname`, `require`, `module`, and `exports` are available in every file without explicit imports.

**Caching — modules are singletons by default:**

```js
// counter.js
let count = 0;
module.exports = { increment: () => ++count };

// a.js and b.js both requiring counter.js get the SAME instance/state
const counterA = require("./counter"); // in a.js
const counterB = require("./counter"); // in b.js — same object as counterA
```

**Circular requires** are supported but return a partial (possibly incomplete) `exports` object at the time of the circular call — a common source of subtle bugs.

**Interview note:** `require()` is **synchronous and blocking** — it reads and executes the file before continuing, which is fine for local/fast module loads but part of why CommonJS doesn't natively support features like top-level `await` the way ES Modules do.
