## Non-blocking code

------
- [ ] **Ensure that code does not block**
- [ ] **Ensure that all I/O is asynchronous except in limited cases**
- [ ] **Use promises for all asynchronous code - convert callbacks to promises if needed**
------

### Event-loop
It is worth the investment to understand the [javascript event loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop), especially if you're coming from other languages. One of the primary selling points of node has always been the asynchronous nature of the code: any blocking operations would prevent other requests from being processed and so all code makes use of callbacks and/or promises.

### Blocking I/O
The node core library provides some methods which are deliberately synchronous e.g. `fs.existsSync` or `fs.readFileSync`. These methods are meant to be used only when absolutely required (when there is a possibility of a race condition that affects the application logic). All other I/O is meant to be asynchronous so that the process can be freed up to process other requests or functions in the queue.

#### Acceptable use-cases for synchronous I/O

* Loading configuration on application startup
* Avoiding race conditions with the file system e.g. Reading files or directories while other processes are able to write to them.

#### Unacceptable use-cases for synchronous I/O

* Loading files from the file system into memory in full before streaming them out
* Making requests to a different back-end


### Promises
[Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises) allow us to perform asynchronous actions in javascript. In a callback we supply a function that takes one argument for errors followed by arguments for responses. In contrast a promise returns an object called a "thenable" which allows us to chain calls to the `.then` method: each call to this method takes two callbacks: one for success and one for errors.

One immediate benefit of promises is that each function invocation is wrapped in a try/catch so that exceptions within the callback functions are also propagated via the thenables.

Promises also allow for errors to propagate to the error handlers. In the case where we have a function call proceeded by 4 `.then` calls, an error anywhere in the chain is propagated to the very first occurrence of an error handler anywhere in the chain.

Error handlers can choose to rethrow the error  to the next error handler, or to return a value which then propagates to the next thenable.
