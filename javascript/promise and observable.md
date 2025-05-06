# Promises (one value, one time)
A `Promise` is used for a single asynchronous value that arrives in the future.
|  |  |
|--|--|
| `new Promise()` | Creates a new Promise and provides `resolve`/`reject` |
| `resolve(value)` | Completes the Promise successfully |
| `reject(error)` | Fails the Promise with an error |
| `then()` | Runs when the Promise is resolved |
| `catch()` | Runs if the Promise is rejected |
| `finally()` | Runs after the Promise is settled (success or failure) |
| `await` | Pauses `async` function until the Promise resolves/rejects |
| `async` | Declares a function that returns a Promise and can use . |
# Observables (multiple values over time)
An `Observable` is a stream that can emit multiple values, and you subscribe to receive them.
|  |  |
|--|--|
| `Observable` | A class from RxJS that represents a stream |
| `subscribe()` | Starts listening to the Observable's emissions |
| `next(value)` | Emits a new value to subscribers |
| `error(err)` | Sends an error to subscribers and stops the stream |
| `complete()` | Signals that the Observable has finished emitting values |
| `unsubscribe()` | Stops receiving values and cleans up resources |
| `pipe()` | Chains RxJS operators to transform the stream |
| `map`, `filter`, `debounceTime`, etc. | Common RxJS operators for stream transformation |
# When working with them at once
Promise callbacks run before Observable emissions, but not because of the order in the code - it's because **Promises use the microtask queue**, and **Observables (usually) use the macrotask queue**.
> **Synchronous code runs first** (top of the stack).
> Then, the **microtask queue** runs: `Promise.then`, `await`, etc.    
>Finally, the **macrotask queue** runs: `setTimeout`, `setInterval`, many Observables (`fromEvent`, `interval`, etc.).

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0OTA2ODQyNDddfQ==
-->