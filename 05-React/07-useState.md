🔹 useState
Used to add local state to a functional component.

JavaScript
import { useState } from 'react';

export default function ToggleSwitch() {
const [isOn, setIsOn] = useState(false);

return (
<button
onClick={() => setIsOn(!isOn)}
style={{ backgroundColor: isOn ? 'green' : 'red', color: 'white', padding: '10px' }} >
{isOn ? 'ON' : 'OFF'}
</button>
);
}
