Q1: What is the Call Stack, and how does it manage program execution?
Answer:
The Call Stack is a LIFO (Last In, First Out) stack structure used to manage execution contexts.

When a function is called, a brand new execution context is pushed onto the top of the stack. When that function hits a return statement, its context is popped off completely, and the engine resumes execution where it left off in the previous underlying context.

┌───────────────────────────────┐
│ three() Execution Context │ <-- 3. Currently executing
├───────────────────────────────┤
│ two() Execution Context │ <-- 2. Paused, waiting for three()
├───────────────────────────────┤
│ one() Execution Context │ <-- 1. Paused, waiting for two()
├───────────────────────────────┤
│ Global Execution Context │ <-- Default base layer
