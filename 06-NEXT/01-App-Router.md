─── 1. Architecture & Routing ───
🔹 App Router
Next.js features a file-system based router built on top of React Server Components called the App Router. It operates inside the app/ directory. Files named page.js (or .tsx) map directly to unique public URL paths.

Plaintext
// App Router Directory Structure Example:
app/
├── layout.js // Root layout shared across all pages
├── page.js // Homepage (/)
├── about/
│ └── page.js // About page (/about)
└── blog/
├── [id]/
│ └── page.js // Dynamic route (/blog/1, /blog/abc)
└── page.js // Blog list page (/blog)
