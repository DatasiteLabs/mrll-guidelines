## Using Logging

------
- [ ] **use Winston for logging**
- [ ] **initialize winston**
------

Winston is a fairly robust and mature solution for logging. It should be used in all cases, even where the logs are being handled by the process manager.

### Severity levels
Out of the box, Winston comes with the same severity levels as `console`: debug, log, error, etc. It can be configured with custom severity levels as well, in cases where we want more control over handling the log call e.g. a severity of `catastrophic` that triggers an email to be dispatched.

### Transports
Winston has a concept of transports: these are outlets for logs and can be configured to only output a message for a minimum severity level. Out of the box it is configured to a single transport for `stdout` but it is possible to also log ot files and remote endpoints.

The recommendation is to use custom severity levels but only use the `stdout` or `console` transport. We can then handle these in PM2 for better visibility.
