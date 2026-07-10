🔹 Routing (Dynamic Routes)
Dynamic routing allows you to create flexible URLs by wrapping a folder name in square brackets: [slug].

JavaScript
// app/product/[id]/page.js

// The dynamic segment 'id' is automatically injected into the `params` prop
export default async function ProductPage({ params }) {
const { id } = await params; // Await params in modern Next.js versions

return (

<section>
<h2>Product Details</h2>
<p style={{ fontWeight: 'bold' }}>Viewing Product ID: <span style={{ color: 'coral' }}>{id}</span></p>
</section>
);
}
