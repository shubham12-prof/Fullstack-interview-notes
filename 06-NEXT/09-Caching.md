─── 3. Data Flow & Hybrid Rendering ───
🔹 Caching
Next.js employs a multi-layered caching architecture by default to speed up operations and lower hosting expenses.

Request Memoization: Caches exact fetch API requests across a single component render tree (server-side).

Data Cache: Persists fetched API data across user requests and deployments until manually cleared.

Full Route Cache: Caches statically rendered HTML pages on the server during build cycles.

Router Cache: Client-side cache that stores visited application pages locally in the browser memory temporarily during navigation transitions.

JavaScript
// Opting-out or bypassing Data Caching inside fetch configurations
const rawData = await fetch('https://api.example.com/live-stock', {
cache: 'no-store' // Do not save cache; fetch fresh live data on every request
});

// Revalidating cache data every 60 seconds (Incremental Static Regeneration)
const products = await fetch('https://api.example.com/products', {
next: { revalidate: 60 }
});
