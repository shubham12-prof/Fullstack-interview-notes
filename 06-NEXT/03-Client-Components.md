🔹 Client Components
If you need interactivity (e.g., event listeners like onClick, React hooks like useState, or browser APIs), you must explicitly mark the file as a Client Component by placing the "use client" directive at the very top of the file.

JavaScript
"use client"; // Opts this component into the client-side lifecycle

import { useState } from 'react';

export default function CounterButton() {
const [likes, setLikes] = useState(0);

return (
<button
onClick={() => setLikes(likes + 1)}
style={{ background: 'royalblue', color: 'white', border: 'none', padding: '10px 15px' }} >
❤️ Likes: {likes}
</button>
);
}
