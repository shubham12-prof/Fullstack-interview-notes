─── 5. Top Tech Interview Questions ───
Q1: What is the difference between Shadow DOM and Virtual DOM?
Shadow DOM: A native browser mechanism used primarily in Web Components to isolate styles and scoping of specific DOM branches.

Virtual DOM: A lightweight, pure JavaScript object copy of the actual DOM created by frameworks like React to abstract away expensive DOM interactions.

Q2: What are "Keys" in React lists, and why are they important?
Keys give array elements stable, unique identities. Without keys, React will re-render and re-sort every individual list node in an array sequentially if changes happen. Do not use array index numbers as keys if the array order changes; this can cause severe state rendering bugs.

Q3: Why can't we call Hooks inside loops, conditions, or nested functions?
React relies completely on the order in which Hooks are called on every single render to map data accurately to state. If you put a Hook inside a conditional branch, that sequence order changes, causing internal memory arrays to shift and break state assignments. Always follow the Rules of Hooks: place them strictly at the top level of your component.

Q4: What is the difference between useMemo and useCallback?
useMemo returns and caches the evaluated value of a function result.

useCallback returns and caches the function instance configuration reference itself.
