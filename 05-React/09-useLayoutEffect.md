🔹 useLayoutEffect
Identical to useEffect, but fires synchronously after all DOM mutations but before the browser paints the screen. Use this only when you need to measure DOM elements (like calculating window layout width) to prevent visual flickering.

JavaScript
import { useState, useLayoutEffect, useRef } from 'react';

export default function LayoutMeasure() {
const [width, setWidth] = useState(0);
const divRef = useRef(null);

useLayoutEffect(() => {
// Measures layout synchronously before visual paint
if (divRef.current) {
setWidth(divRef.current.getBoundingClientRect().width);
}
}, []);

return (

<div ref={divRef} style={{ width: '50%', background: 'lightblue', padding: '10px' }}>
My synchronous width is: {width}px
</div>
);
}
