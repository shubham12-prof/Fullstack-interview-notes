# Environment Variables

Key-value configuration passed into a process from its environment, letting the same code run differently across environments (development, staging, production) without hardcoding values or committing secrets to source control.

```js
// Accessing environment variables
console.log(process.env.NODE_ENV); // e.g. 'development', 'production'
console.log(process.env.PORT || 3000); // fallback default if not set
console.log(process.env.DATABASE_URL);
```

**Setting them:**

```bash
# Inline, for a single command
NODE_ENV=production node app.js

# Exported for the whole shell session
export API_KEY=abc123
node app.js
```

**Using a `.env` file (via the `dotenv` package) for local development:**

```js
// .env (NEVER commit this file — add it to .gitignore)
DATABASE_URL=postgres://localhost/mydb
API_KEY=secret123

// app.js
require("dotenv").config(); // loads .env into process.env
console.log(process.env.DATABASE_URL);
```

**Common pattern — centralized, validated config:**

```js
// config.js
function requireEnv(name) {
  const value = process.env[name];
  if (!value) throw new Error(`Missing required environment variable: ${name}`);
  return value;
}

module.exports = {
  port: process.env.PORT || 3000,
  databaseUrl: requireEnv("DATABASE_URL"), // fails fast at startup if missing
  isProduction: process.env.NODE_ENV === "production",
};
```

**Interview note:** environment variables are the standard way to keep secrets (API keys, DB credentials) OUT of source code — committing a `.env` file or hardcoding secrets is a common security mistake; always add `.env` to `.gitignore` and provide a `.env.example` template with placeholder values instead.
