🔹 React.memo
A Higher-Order Component (HOC) used to optimize performance by skipping a component re-render if its input props haven't changed.

JavaScript
import React, { useState } from 'react';

// This component will ONLY re-render if props.name changes
const DisplayName = React.memo(({ name }) => {
console.log('DisplayName component rendered!');
return <h3>Hello, {name}!</h3>;
});

export default function OptimisedApp() {
const [name, setName] = useState('John');
const [counter, setCounter] = useState(0);

return (

<div>
<input value={name} onChange={e => setName(e.target.value)} />
<button onClick={() => setCounter(counter + 1)}>Increment: {counter}</button>
<DisplayName name={name} />
</div>
);
}
