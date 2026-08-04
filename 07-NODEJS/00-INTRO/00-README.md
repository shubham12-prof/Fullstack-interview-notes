# 🟢 Node.js Complete Mastery Guide

> A structured, code-first deep dive into Node.js internals, core modules, and best practices — organized topic by topic, each with explanations, diagrams (ASCII), runnable code, and pitfalls to avoid.

---

## 📚 Table of Contents

| #   | Topic                                   | Folder                                                                 |
| --- | --------------------------------------- | ---------------------------------------------------------------------- |
| 01  | 🏗️ Node Architecture                    | [`01-node-architecture`](./01-node-architecture/README.md)             |
| 02  | 🔁 Event Loop                           | [`02-event-loop`](./02-event-loop/README.md)                           |
| 03  | 📢 EventEmitter                         | [`03-eventemitter`](./03-eventemitter/README.md)                       |
| 04  | 📦 Modules (CommonJS & ES Modules)      | [`04-modules`](./04-modules/README.md)                                 |
| 05  | 📁 File System (`fs`)                   | [`05-file-system`](./05-file-system/README.md)                         |
| 06  | 🧭 Path                                 | [`06-path`](./06-path/README.md)                                       |
| 07  | 🖥️ OS Module                            | [`07-os-module`](./07-os-module/README.md)                             |
| 08  | 🌐 HTTP Module                          | [`08-http-module`](./08-http-module/README.md)                         |
| 09  | 🌊 Streams                              | [`09-streams`](./09-streams/README.md)                                 |
| 10  | 🧮 Buffers                              | [`10-buffers`](./10-buffers/README.md)                                 |
| 11  | ⚙️ Process                              | [`11-process`](./11-process/README.md)                                 |
| 12  | 🧩 Cluster                              | [`12-cluster`](./12-cluster/README.md)                                 |
| 13  | 🧵 Worker Threads                       | [`13-worker-threads`](./13-worker-threads/README.md)                   |
| 14  | 👶 Child Processes                      | [`14-child-processes`](./14-child-processes/README.md)                 |
| 15  | 🔐 Environment Variables                | [`15-environment-variables`](./15-environment-variables/README.md)     |
| 16  | 📦 Package Management (npm, pnpm, yarn) | [`16-package-management`](./16-package-management/README.md)           |
| 17  | 🚨 Error Handling                       | [`17-error-handling`](./17-error-handling/README.md)                   |
| 18  | 📝 Logging                              | [`18-logging`](./18-logging/README.md)                                 |
| 19  | 🛡️ Security Best Practices              | [`19-security-best-practices`](./19-security-best-practices/README.md) |
| 20  | ❓ Interview Questions                  | [`20-interview-questions`](./20-interview-questions/README.md)         |

---

## 🧠 How to Use This Guide

1. Go **in order** if you're learning — each topic builds intuition for the next (Architecture → Event Loop → EventEmitter are foundational).
2. Every folder has a `README.md` with:
   - 🎯 Concept explanation
   - 🖼️ Diagrams (ASCII art where useful)
   - 💻 Full runnable code examples
   - ⚠️ Common pitfalls
   - 🧪 "Try it yourself" exercises
3. Copy-paste the code blocks into a `.js` file and run with `node file.js` (Node.js v18+ recommended).

---

## 🗺️ Node.js Mental Model (Quick Preview)

```
                     ┌─────────────────────────────┐
                     │        Your JS Code          │
                     └───────────────┬──────────────┘
                                     │
                     ┌───────────────▼──────────────┐
                     │      Node.js APIs / Bindings  │
                     │   (fs, http, net, crypto...)  │
                     └───────────────┬──────────────┘
                                     │
        ┌────────────────────────────┼────────────────────────────┐
        │                            │                             │
┌───────▼────────┐         ┌─────────▼─────────┐         ┌─────────▼────────┐
│   V8 Engine     │         │     libuv          │         │  C++ Bindings    │
│ (executes JS)   │         │ (event loop, I/O,   │         │ (OS-level calls) │
│                 │         │  thread pool)       │         │                  │
└─────────────────┘         └─────────────────────┘         └──────────────────┘
```

---

## ⭐ Quick Start Cheat Sheet

```bash
node -v                # check Node version
node app.js            # run a script
node --watch app.js    # auto-restart on file change (Node 18+)
npm init -y             # create package.json
npm install express      # install a dependency
node --inspect app.js    # debug with Chrome DevTools
```

---

Happy learning! 🚀 Every topic is self-contained — jump straight to what you need.
