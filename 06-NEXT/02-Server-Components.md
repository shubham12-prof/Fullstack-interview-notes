🔹 Server Components (RSC)
By default, all components inside the App Router are React Server Components. They are compiled exclusively on the server.

Benefits: Zero impact on client-side JavaScript bundle size, direct access to backend resources (databases, APIs), and superior SEO.

JavaScript
// app/users/page.js
// This code runs entirely on the server. You can safely fetch data or read files!
export default async function UsersPage() {
const response = await fetch('https://jsonplaceholder.typicode.com/users');
const users = await response.json();

return (

<main style={{ padding: '20px' }}>
<h1>👥 System Users</h1>
<ul>
{users.map(user => (
<li key={user.id} style={{ color: 'teal', margin: '5px 0' }}>
{user.name} ({user.email})
</li>
))}
</ul>
</main>
);
}
