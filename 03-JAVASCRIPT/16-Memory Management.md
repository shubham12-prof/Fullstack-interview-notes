16. Memory Management
    Q1: How does JavaScript handle Memory Management, and what causes Memory Leaks?
    Answer:
    JavaScript allocates memory automatically when variables are initialized and releases it via a background process called Garbage Collection using a "Mark-and-Sweep" algorithm. Memory blocks that become entirely unreachable from the global root window are safely swept away.

Common sources of Memory Leaks:

Accidental Global Variables: Initializing variables without block declarations binds them to the global root object permanently, preventing clean garbage collection.

Forgotten Event Listeners: Mounting event listeners onto DOM nodes without removing them keeps any wrapped scope closure variables alive indefinitely.
