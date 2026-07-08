🔹 useMemo
Returns a memoized value. It optimizes performance by caching the result of an expensive calculation across re-renders, recalculating only when one of its dependencies changes.

JavaScript
import { useState, useMemo } from 'react';

export default function ExpensiveCalculationExample() {
const [count, setCount] = useState(0);
const [text, setText] = useState('');

// Simulating an expensive function
const expensiveValue = useMemo(() => {
console.log('Calculating complex math...');
let total = 0;
for (let i = 0; i < 100000000; i++) { total += i; }
return total + count;
}, [count]); // Only recalculates when 'count' changes. Changing 'text' won't trigger this!

return (

<div>
<h3>Result: {expensiveValue}</h3>
<button onClick={() => setCount(count + 1)}>Increment Count</button>
<input value={text} onChange={(e) => setText(e.target.value)} placeholder="Type something..." />
</div>
);
}
