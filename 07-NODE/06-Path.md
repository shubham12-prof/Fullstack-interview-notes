# Path

The built-in module for working with file and directory paths in a platform-independent way (handles differences between POSIX `/` and Windows `\` separators automatically).

```js
const path = require("path");

path.join("/users", "alice", "docs", "file.txt");
// "/users/alice/docs/file.txt" — normalizes slashes, resolves '..' and '.'

path.resolve("folder", "file.txt");
// absolute path, resolved against the current working directory

path.basename("/users/alice/file.txt"); // "file.txt"
path.basename("/users/alice/file.txt", ".txt"); // "file" — strip extension too
path.dirname("/users/alice/file.txt"); // "/users/alice"
path.extname("/users/alice/file.txt"); // ".txt"

path.parse("/users/alice/file.txt");
// { root: '/', dir: '/users/alice', base: 'file.txt', ext: '.txt', name: 'file' }

path.isAbsolute("/users/alice"); // true
path.isAbsolute("alice/docs"); // false

path.sep; // '/' on POSIX, '\' on Windows — the platform's path separator
```

**`path.join` vs `path.resolve`:**

|                   | join                                        | resolve                                                          |
| ----------------- | ------------------------------------------- | ---------------------------------------------------------------- |
| Result            | concatenates + normalizes segments as given | always returns an ABSOLUTE path                                  |
| Relative segments | kept relative                               | resolved against `process.cwd()` (or preceding absolute segment) |

```js
path.join("a", "b"); // "a/b" (relative)
path.resolve("a", "b"); // "/current/working/dir/a/b" (absolute)
```

**Interview note:** always use `path.join`/`path.resolve` instead of manually concatenating strings with `/` — this avoids cross-platform bugs (Windows uses `\`) and correctly handles edge cases like trailing slashes or `..` segments.
