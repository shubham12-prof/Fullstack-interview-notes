Q1: What is an Execution Context, and what are its phases?
Answer:
An Execution Context is an environment created by the engine to manage the execution of code. It acts as a wrapper containing the running code, local variables, and the dynamic value of this. It runs in two distinct phases:

Creation Phase: The compiler allocates memory space for variables and functions (hoisting) and builds the outer environment scope link.

Execution Phase: The engine executes the code line by line, assigning actual values and running function blocks.
