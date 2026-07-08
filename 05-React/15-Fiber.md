─── 4. Advanced Core Mechanics ───
🔹 Fiber
React Fiber is the underlying engine rewrite introduced in React 16. It changed React's rendering from a synchronous execution engine to an asynchronous, cooperative scheduler.

Old Engine (Stack Reconciler): Render processes were synchronous and blocking. If a complex tree was rendering, the UI would freeze until complete.

Fiber Engine: Breaks work down into tiny units called "fibers". It can pause execution work, yield control back to the browser main thread to handle user inputs/animations, and resume rendering right where it left off.
