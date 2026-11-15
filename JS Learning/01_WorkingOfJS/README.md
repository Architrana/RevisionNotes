# How JavaScript Works

## From source code to execution

JavaScript engines (such as V8) parse and execute JavaScript. Modern engines may compile code just in time (JIT) and optimize frequently used paths.

When a script starts, the engine creates an **execution context**. It keeps track of the current code, its variables, and the value of `this`. A function call creates a new function execution context.

Declarations have different initialization behavior:

- `var` declarations are initialized to `undefined` when their scope is prepared.
- `let` and `const` are unavailable in the temporal dead zone until their declaration is evaluated.
- Function declarations can generally be called before their position in the source.

## Call stack and memory

The **call stack** tracks active function calls. A call adds a frame; returning removes it. Unbounded or very deep recursion can cause a stack overflow.

Values are stored in engine-managed memory. Objects and functions are accessed through references, and garbage collection reclaims objects that are no longer reachable.

## Asynchronous JavaScript

JavaScript runs synchronous code on a call stack, one operation at a time. The browser or Node.js host provides APIs for timers, I/O, and other work. When that work completes, callbacks are placed in queues.

- **Tasks** (often called macrotasks) include timer callbacks and many I/O callbacks.
- **Microtasks** include promise handlers and callbacks scheduled with `queueMicrotask`.

When the current stack is empty, the event loop drains microtasks before starting the next task. A timer delay is a minimum wait, not a guarantee of exact timing.

```js
console.log("A");
setTimeout(() => console.log("C"), 0);
Promise.resolve().then(() => console.log("B"));
console.log("D");

// Output: A, D, B, C
```

## In short

The engine executes JavaScript, the host environment supplies APIs, and the event loop coordinates queued asynchronous callbacks.

## Reference
[Visual understanding of JS working](https://latentflip.com/loupe/?code=JC5vbignYnV0dG9uJywgJ2NsaWNrJywgZnVuY3Rpb24gb25DbGljaygpIHsKICAgIHNldFRpbWVvdXQoZnVuY3Rpb24gdGltZXIoKSB7CiAgICAgICAgY29uc29sZS5sb2coJ1lvdSBjbGlja2VkIHRoZSBidXR0b24hJyk7ICAgIAogICAgfSwgMjAwMCk7Cn0pOwoKY29uc29sZS5sb2coIkhpISIpOwoKc2V0VGltZW91dChmdW5jdGlvbiB0aW1lb3V0KCkgewogICAgY29uc29sZS5sb2coIkNsaWNrIHRoZSBidXR0b24hIik7Cn0sIDUwMDApOwoKY29uc29sZS5sb2coIldlbGNvbWUgdG8gbG91cGUuIik7!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D)
