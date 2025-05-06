# Promises (one value, one time)
A `Promise` is used for a single asynchronous value that arrives in the future.
|  |  |
|--|--|
|  |  |

Keyword

Meaning

`new Promise()`

Creates a new Promise and provides `resolve`/`reject`.

`resolve(value)`

Completes the Promise successfully.

`reject(error)`

Fails the Promise with an error.

`then()`

Runs when the Promise is resolved.

`catch()`

Runs if the Promise is rejected.

`finally()`

Runs after the Promise is settled (success or failure).

`await`

Pauses `async` function until the Promise resolves/rejects.

`async`

Declares a function that returns a Promise and can use `await`.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA1NzI0NTM3N119
-->