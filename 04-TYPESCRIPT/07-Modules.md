6. Modules
   Q1: How does TypeScript handle Modules, and what is the difference between import type and a standard import?
   Answer:
   TypeScript follows the modern ES6 module standard (import/export). However, it introduces a specialized syntax: import type.

Standard Import (import { User } from './types'): The compiler imports the reference. If the file contains mixed code (classes and types), it leaves the import statement inside the output file.

import type: Guarantees that the imported target is completely stripped out of your final JavaScript output bundle. It is used exclusively for type annotations and avoids loading unnecessary modules at runtime.

TypeScript
import type { LargeUserInterface } from "./interfaces";
import { userService } from "./services";

// Code Explanation:
// 'LargeUserInterface' is stripped entirely from the final JS file during bundling.
// 'userService' remains in the compiled JS code because it contains real executable logic.
