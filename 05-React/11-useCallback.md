🔹 useCallback
Returns a memoized version of a callback function. It is used to prevent child components from unnecessarily re-rendering if they rely on a function prop that gets recreated on every parent re-render.

JavaScript
import { useState, useCallback } from 'react';

// Child component
const Button = React.memo(({ handleClick }) => {
console.log('Button rendered!');
return <button onClick={handleClick}>Click Me</button>;
});

// Parent component
export default function ParentComponent() {
const [count, setCount] = useState(0);

// Caches the function instance
const increment = useCallback(() => {
setCount(prev => prev + 1);
}, []); // Empty dependency ensures function reference stays identical

return (

<div>
<h2>Count: {count}</h2>
<Button handleClick={increment} />
</div>
);
}
