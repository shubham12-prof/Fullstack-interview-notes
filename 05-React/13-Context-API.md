─── 3. Global State & Optimization ───
🔹 Context API
Provides a clean way to pass data down the component tree without manually passing props through every single level (avoiding "prop drilling").

JavaScript
import { createContext, useContext, useState } from 'react';

// 1. Create Context
const ThemeContext = createContext();

export function ThemeProvider({ children }) {
const [theme, setTheme] = useState('light');
return (
<ThemeContext.Provider value={{ theme, setTheme }}>
{children}
</ThemeContext.Provider>
);
}

// 2. Consume Context inside a deep nested child
export default function ThemeButton() {
const { theme, setTheme } = useContext(ThemeContext);
return (
<button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
Current Theme: {theme.toUpperCase()}
</button>
);
}
