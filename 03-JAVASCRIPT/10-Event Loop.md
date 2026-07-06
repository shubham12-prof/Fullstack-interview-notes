Q1: What is the Event Loop, and how does JavaScript manage asynchronous code?
Answer:
JavaScript runs tasks sequentially on a single thread via its Call Stack. It handles asynchronous tasks (like network calls or timers) by handing them off to the browser's native background Web APIs environment.

When a background Web API finishes, its callback function is dropped into a task queue. The Event Loop continuously monitors the engine. The exact millisecond the Call Stack becomes completely empty, the Event Loop takes the first waiting callback from the queue and pushes it onto the Call Stack to run.
