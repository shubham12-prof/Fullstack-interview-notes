🔹 useEffect
Used to perform side effects (data fetching, subscriptions, manual DOM updates) in functional components.

JavaScript
import { useState, useEffect } from 'react';

export default function DataFetcher() {
const [data, setData] = useState([]);

useEffect(() => {
// 1. Mount / Effect logic
fetch('https://jsonplaceholder.typicode.com/users')
.then(res => res.json())
.then(data => setData(data));

    // 2. Unmount / Optional Cleanup logic
    return () => console.log('Component unmounted or dependencies changed!');

}, []); // [] means this runs exactly ONCE when the component mounts.

return (

<ul>
{data.slice(0, 3).map(user => <li key={user.id}>{user.name}</li>)}
</ul>
);
}
