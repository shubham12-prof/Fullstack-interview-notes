## Q1: What is the difference between a shallow copy and a deep copy in JavaScript?

Answer:

## Shallow Copy:

Copies only the top-level primitive values of an object. If the object contains nested objects, it copies the memory references to those nested objects instead of duplicating them. Modifying a deep nested property in the copy will accidentally modify the original object. (Created via {...obj}).

## Deep Copy:

Clones every single level of the target object structure recursively. It creates completely distinct values and decoupled nested paths in memory space. (Modern standard standard approach is structuredClone(obj)).
