# Logging

Recording application behavior and errors for debugging, monitoring, and auditing — production Node apps typically use a structured logging library instead of plain `console.log`.

**Why not just `console.log` in production?**

- No log levels (can't easily filter debug vs error logs)
- No structured format (hard to parse/query in log aggregation tools like Datadog, ELK, Splunk)
- Synchronous by default in some environments — can impact performance under high volume
- No built-in support for log rotation, file output, or contextual metadata

**Using a structured logger (Pino — one of the fastest Node loggers):**

```js
const pino = require("pino");
const logger = pino({ level: process.env.LOG_LEVEL || "info" });

logger.info({ userId: 123 }, "User logged in");
logger.warn("Cache miss for key: user:123");
logger.error({ err }, "Failed to process payment");

// Output is structured JSON — easy for log aggregation tools to parse:
// {"level":30,"time":..., "userId":123, "msg":"User logged in"}
```

**Log levels (standard convention, lowest to highest severity):**

```
trace < debug < info < warn < error < fatal
```

Setting a level (e.g., `info`) suppresses lower-severity logs (like `debug`/`trace`) in production while keeping them available in development.

**Request logging middleware (Express + morgan or pino-http):**

```js
const pinoHttp = require("pino-http");
app.use(pinoHttp()); // logs method, URL, status code, response time for every request automatically
```

**Good logging practices:**

- Log structured data (objects), not just interpolated strings — makes logs queryable.
- Never log sensitive data (passwords, tokens, full credit card numbers).
- Include correlation/request IDs so logs from one request can be traced across services.
- Send logs to a centralized aggregation system in production, not just local files.

**Interview note:** "Why prefer structured logging over `console.log`?" — structured (JSON) logs can be indexed, filtered, and queried at scale by log aggregation tools, support log levels for noise control, and typically offer better performance characteristics (async writes, lower overhead) than repeated synchronous `console.log` calls under high load.
