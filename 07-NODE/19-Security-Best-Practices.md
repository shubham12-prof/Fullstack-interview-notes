# Security Best Practices

Common vulnerabilities and mitigations specific to Node.js backend applications.

**1. Never trust user input — validate and sanitize everything:**

```js
const { z } = require("zod");
const userSchema = z.object({
  email: z.string().email(),
  age: z.number().min(0),
});
const result = userSchema.safeParse(req.body);
if (!result.success) return res.status(400).json({ error: result.error });
```

**2. Prevent SQL injection — use parameterized queries, never string concatenation:**

```js
// ❌ DANGEROUS — vulnerable to SQL injection
db.query(`SELECT * FROM users WHERE email = '${email}'`);

// ✅ SAFE — parameterized query
db.query("SELECT * FROM users WHERE email = ?", [email]);
```

**3. Prevent shell injection — avoid `exec()` with unsanitized input (see Child Processes file):**

```js
// ❌ DANGEROUS
exec(`convert ${filename} output.png`);
// ✅ SAFER — arguments passed as an array, not interpolated into a shell string
execFile("convert", [filename, "output.png"]);
```

**4. Set security-related HTTP headers (via `helmet` in Express):**

```js
const helmet = require("helmet");
app.use(helmet()); // sets X-Content-Type-Options, X-Frame-Options, CSP defaults, etc.
```

**5. Rate limiting — protect against brute-force and denial-of-service:**

```js
const rateLimit = require("express-rate-limit");
app.use(rateLimit({ windowMs: 15 * 60 * 1000, max: 100 })); // 100 requests per 15 min per IP
```

**6. Never hardcode secrets — use environment variables (see that file), and never log them.**

**7. Keep dependencies updated and audit for known vulnerabilities:**

```bash
npm audit
npm audit fix
```

**8. Hash passwords properly — never store plaintext, use a slow, salted hash:**

```js
const bcrypt = require("bcrypt");
const hashed = await bcrypt.hash(password, 12); // 12 = cost factor (salt rounds)
const isValid = await bcrypt.compare(password, hashed);
```

**9. Use HTTPS in production, and set secure cookie flags:**

```js
res.cookie("session", token, {
  httpOnly: true,
  secure: true,
  sameSite: "strict",
});
```

**10. Limit payload size to prevent denial-of-service via huge request bodies:**

```js
app.use(express.json({ limit: "1mb" }));
```

**Interview note:** a strong answer to "how do you secure a Node API?" touches multiple layers — input validation, parameterized queries, security headers, rate limiting, secret management, dependency auditing, and password hashing — rather than naming just one technique. Security is defense-in-depth, not a single fix.
