🔹 Reconciliation
The algorithm React uses to update the browser DOM. It builds a Virtual DOM tree, compares it to an updated Virtual DOM tree when state changes (a process called Diffing), and calculates the absolute minimum number of updates required to match the new state.

📝 The Diffing Rules:

Elements of different types will tear down the old tree and build a completely new one.

Elements of the same type check attributes/props and modify only changed attributes.

Keys help React uniquely track dynamic array elements to minimize layout thrashing.
