🔹 Props (Properties)
Props are read-only inputs passed from a parent component to a child component. They allow components to be dynamic and reusable. Props are immutable—a child component must never modify its own props.

JavaScript
// Child Component extracting props using object destructuring
function UserCard({ name, role }) {
return (

<div style={{ border: '1px solid #ccc', padding: '10px', borderRadius: '5px' }}>
<h3>👤 Name: {name}</h3>
<p>💼 Role: {role}</p>
</div>
);
}

// Parent Component
export default function ProfilePage() {
return (

<div>
<UserCard name="Alice" role="Frontend Engineer" />
<UserCard name="Bob" role="UI Designer" />
</div>
);
}
