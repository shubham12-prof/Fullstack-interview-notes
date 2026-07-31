# EventEmitter

The foundational class behind Node's event-driven architecture — many built-in objects (HTTP servers, streams, process) extend `EventEmitter`. Implements the Observer pattern: register listeners with `.on()`, fire them with `.emit()`.

```js
const EventEmitter = require("events");

class OrderService extends EventEmitter {
  placeOrder(order) {
    // ... process order ...
    this.emit("orderPlaced", order); // notify all listeners
  }
}

const orders = new OrderService();

orders.on("orderPlaced", (order) => {
  console.log(`Sending confirmation email for order #${order.id}`);
});
orders.on("orderPlaced", (order) => {
  console.log(`Updating inventory for order #${order.id}`);
});

orders.placeOrder({ id: 123 }); // triggers BOTH listeners, in registration order
```

**Key methods:**

```js
emitter.on(event, listener); // register a listener (can register many for the same event)
emitter.once(event, listener); // listener fires only once, then auto-removed
emitter.off(event, listener); // remove a specific listener
emitter.removeAllListeners(event); // remove all listeners for an event
emitter.emit(event, ...args); // trigger the event, passing args to listeners
emitter.listenerCount(event); // number of registered listeners
```

**The special `'error'` event:** if an `EventEmitter` emits `'error'` with no registered listener, Node **throws** the error and crashes the process — always register an error handler.

```js
emitter.on("error", (err) => console.error("Handled:", err.message));
emitter.emit("error", new Error("Something broke")); // safely caught, no crash
```

**Interview note:** listeners are called **synchronously, in the order they were registered** — `emit()` doesn't return until all listeners have finished running (unless a listener itself does async work internally). By default, Node warns if more than 10 listeners are added to a single event (a common memory-leak indicator) — configurable via `emitter.setMaxListeners(n)`.
