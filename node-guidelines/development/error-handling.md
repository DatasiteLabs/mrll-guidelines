## Error handling

------
- [ ] **Ensure that exceptions are caught and minimize UncaughtExceptions**
- [ ] **Ensure that promises have an error handler at the root of the promise chain**
- [ ] **Use custom Errors to help with managing Errors**
------

### Promises
Ensure that promise errors are caught. Any unhandled failed promises are treated as uncaught exceptions, and in future node versions will crash the process. See DEP0018 in the node documentation.

In the following example, note that we don't have an error handler for the promise.

```javascript
router.get('/', (req, res) => {
  return asyncGetResource() <1>
    .then(resource => res.json(resource));
}
```
<1> If `asyncGetResource` were to throw an error, then the request would time out. Why? There is no error handler for the promise, so this middleware never sends a response and will eventually timeout. On the server there would be a warning generated about unhandled exceptions along with a deprecation warning.

#### A correct implementation
```javascript
router.get('/', (req, res) => {
  return asyncGetResource()
    .then((resource: Response) => res.json(resource))
    .catch(err => {
      // log the error
      res.status(500).end();
    });
}
```

### Global error handler
Ensure that there is a global error handler for express. This is identified by a middleware that takes 4 arguments - it must be exactly 4. This gets called whenever `next()` is called with an error (e.g. in authentication middleware). Use custom Errors here to display the appropriate error to the user.

```javascript
app.use((err, req, resp, next) => {
  // log the error, return status code of 500
});
```

> **This must be the last middleware registered with Express for it to work as intended.**

### UncaughtExceptions
Ensure that uncaught exceptions are handled but that the process still exits. This is the place to perform cleanup and to log the exception.

```javascript
process.on('uncaughtException', (err: Error) => {
  // Perform some safe synchronous clean-up here if needed.
  // Avoid anything that might throw other exceptions.
  process.exit(1); <1>
})
```
<1> Ensure that the process exits
