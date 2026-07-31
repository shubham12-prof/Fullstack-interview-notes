# Behavioral Questions & Interview Tips

## Common Follow-Up / Deep-Dive Questions

- "Walk me through what happens when a request comes into a Node HTTP server and hits a slow database query." (event loop stays free during the async DB call → other requests keep being processed → callback/Promise resolves → response sent)
- "How would you scale a Node app to use all CPU cores on a machine?" (Cluster module, or a process manager like PM2 in cluster mode; discuss stateless design implications)
- "How would you debug a memory leak in a long-running Node process?" (heap snapshots via `--inspect`/Chrome DevTools, comparing snapshots over time, checking for growing caches/unclosed listeners/timers)
- "How would you handle a CPU-intensive task without blocking incoming requests?" (Worker Threads, or offload to a separate service/queue)
- "Describe how you'd design graceful shutdown for a Node service running in Kubernetes." (listen for SIGTERM, stop accepting new connections, finish in-flight requests, close DB connections, then exit)
- "What's your approach to structuring error handling across a large Express API?" (centralized error-handling middleware, custom error classes with status codes, consistent logging)

## Tips for the Interview

- When asked to trace event loop output, separate work into: sync code → `process.nextTick` → Promise microtasks → macrotask phases (timers → poll → check) — this order is a very common whiteboard question.
- For architecture questions (Cluster vs Worker Threads, exec vs spawn), always state the underlying tradeoff (process isolation vs shared memory; buffered vs streamed output) rather than just naming the tools.
- When discussing security, mention defense-in-depth (validation, parameterized queries, headers, rate limiting) rather than a single technique — interviewers often probe whether you understand it's layered.
- If unsure about a low-level detail (e.g., exact libuv thread pool size), say what you know confidently and reason through the rest — demonstrating problem-solving process matters as much as memorized facts.
