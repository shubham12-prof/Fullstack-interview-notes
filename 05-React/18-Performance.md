🔹 Performance Checklist
Prevent Unnecessary Re-renders: Wrap static component configurations in React.memo().

Cache Inline Handlers: Use useCallback to stop child re-renders on object or function changes.

Lazy Loading: Dynamically import heavy features using React.lazy() and <Suspense>.

Windowing / Virtualization: Use tools like react-window for processing large list arrays instead of drawing thousands of nodes down to the DOM at once.
