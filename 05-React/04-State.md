🔹 State
State represents the local, dynamic memory of a component. Unlike props, state is mutable (via its setter function) and managed completely inside the component. When state changes, React automatically re-renders the component.

JavaScript
import { useState } from 'react';

export default function Counter() {
// Declaring a state variable named 'count' initialized to 0
const [count, setCount] = useState(0);

return (

<div style={{ textAlign: 'center', marginTop: '20px' }}>
<h2>🔢 Count: {count}</h2>
<button onClick={() => setCount(count + 1)}>Increment</button>
<button onClick={() => setCount(count - 1)} style={{ marginLeft: '10px' }}>Decrement</button>
</div>
);
}
