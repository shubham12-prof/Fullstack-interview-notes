🔹 Modules (CommonJS & ES Modules)Node.js supports two module systems. Modern applications prefer ES Modules (ESM).FeatureCommonJS (CJS)ES Modules (ESM)Extension.js (default) or .cjs.mjs (or .js with "type": "module" in package.json)Syntaxrequire() / module.exportsimport / exportExecutionSynchronous (at runtime)Asynchronous (statically parsed)JavaScript// ====== CommonJS (math.cjs) ======
const add = (a, b) => a + b;
module.exports = { add };

// Loading CommonJS
const { add } = require('./math.cjs');

// ====== ES Modules (math.mjs) ======
export const multiply = (a, b) => a \* b;

// Loading ES Modules
import { multiply } from './math.mjs';
