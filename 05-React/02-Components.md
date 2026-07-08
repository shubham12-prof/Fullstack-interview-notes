🔹Components
Components are the building blocks of a React application. They are reusable, independent pieces of UI. They must start with a capital letter and return JSX.

JavaScript
// 1. Functional Component (Modern Standard)
function WelcomeMessage() {
return <h2>Welcome to the React Guide!</h2>;
}

// 2. Parent Component rendering the child
export default function App() {
return (

<main>
<h1>Dashboard</h1>
<WelcomeMessage />
</main>
);
}
