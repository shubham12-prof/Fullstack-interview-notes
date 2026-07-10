## Q1: What happens when a component with "use client" imports a Server Component?

This is a standard trap question. A Server Component cannot be imported directly inside a Client Component. If you do this, Next.js will automatically convert that Server Component into a Client Component and ship it down to the browser anyway.

The Solution: To render a Server Component inside a Client Component correctly, pass it down cleanly as a children prop.

## Q2: How does data fetching differ between Next.js App Router and the older Pages Router?

Pages Router: Relies on structural boilerplate methods outside components like getStaticProps or getServerSideProps to fetch data.

App Router: Fully implements async/await directly inside standard React Server Components, removing legacy lifecycle abstractions and enabling granular native fetch() optimizations.

## Q3: What is the purpose of the layout.js file vs a template.js file?

layout.js: Persists its UI across routing navigation transitions and avoids re-rendering. It preserves stateful UI data (like open sidebars or filled inputs).

template.js: Creates a completely unique component instance configuration for every route visit. It forces elements to rebuild completely, triggering fresh entry animations or execution blocks on every navigation change.

## Q4: How do you force a Next.js route to be completely dynamic instead of static?

By default, Next.js analyzes your code structure and caches pages automatically if no dynamic operations are present. You can explicitly force a route to evaluate dynamically on every single request using route segment configuration values:

JavaScript
export const dynamic = 'force-dynamic'; // Insert this export at the top of your page.js file
