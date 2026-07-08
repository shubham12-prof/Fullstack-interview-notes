🔹 useRef
Returns a mutable ref object whose .current property persists across re-renders. Crucially, modifying .current does not cause a re-render. It is used for direct DOM access or storing persistent mutable variables.

JavaScript
import { useRef } from 'react';

export default function FocusInput() {
const inputRef = useRef(null);

const focusTextBox = () => {
// Direct access to the native DOM node
inputRef.current.focus();
inputRef.current.style.backgroundColor = '#fff9c4';
};

return (

<div>
<input ref={inputRef} type="text" placeholder="Click button to focus..." />
<button onClick={focusTextBox} style={{ marginLeft: '10px' }}>Focus Now</button>
</div>
);
}
