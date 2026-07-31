# ES Modules

The standardized JS module system (`import`/`export`), now natively supported in Node (in addition to browsers). Statically analyzable (imports/exports are resolved at parse time, not runtime), which enables tree shaking and top-level `await`.

**Enabling ESM in Node** — either:

```json
// package.json
{ "type": "module" }
```

or use the `.mjs` file extension (CommonJS files can use `.cjs` explicitly if the package default is `"type": "module"`).

```js
// math.mjs
export function add(a, b) {
  return a + b;
}
export const PI = 3.14159;
export default function multiply(a, b) {
  return a * b;
}

// main.mjs
import multiply, { add, PI } from "./math.mjs";
console.log(add(2, 3)); // 5

// Top-level await — works directly in ESM, NOT in CommonJS
const data = await fetch("https://api.example.com/data").then((r) => r.json());
```

**Dynamic import (works in both module systems, always async):**

```js
const math = await import("./math.mjs");
```

**Key differences from CommonJS:**

|                          | CommonJS                                | ES Modules                                    |
| ------------------------ | --------------------------------------- | --------------------------------------------- |
| Syntax                   | `require()` / `module.exports`          | `import` / `export`                           |
| Loading                  | synchronous                             | asynchronous (supports top-level await)       |
| Analysis                 | dynamic (can `require()` conditionally) | static (imports resolved at parse time)       |
| `this` at top level      | `module.exports`                        | `undefined`                                   |
| `__dirname`/`__filename` | available                               | NOT available (use `import.meta.url` instead) |

```js
// ESM equivalent of __dirname
import { fileURLToPath } from "url";
import { dirname } from "path";
const __filename = fileURLToPath(import.meta.url);
const __dirname = dirname(__filename);
```

**Interop:** ESM can `import` CommonJS modules (getting the whole `module.exports` as the default export), but CommonJS's `require()` cannot synchronously load a pure ESM module — you'd need dynamic `import()` instead.

**Interview note:** the biggest practical reason to prefer ESM in new Node projects is tooling alignment (matches browser/bundler behavior, enables tree shaking) and top-level `await` — but many existing npm packages and codebases still ship CommonJS, so interop knowledge matters.
