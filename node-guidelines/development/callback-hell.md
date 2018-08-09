## Callback hell

------
- [ ] **embrace the functional nature of javascript: write small and single-purpose functions**
- [ ] **consider using named functions instead of lambdas**
- [ ] **favour promises over callbacks**
- [ ] **if you use async/await, ensure that errors are handled**
------

"Callback hell" refers to a readability concern when working with nested callbacks. Since a callback is passed into a function in order to carry out the next asynchronous operation, a multi-step asynchronous process would produce multiple levels of indentation.

Consider the following example which checks a user's password in a two-step process: fetching the user and then checking the password.

```javascript
// NB: callbacks for illustration purpose only!
function checkPass(password, cb) {
  getUserById(id, (userErr, user) => { <1>
    if (userErr) return cb(new UserFailedError()); <2>

    compareUserPassword(user.password, password, (locationErr, location) => {
      if (locationErr) return cb(PasswordCheckFailedError()); <3>

      cb(getFilteredProps(user));
    });
  });
}
```
<1> Indentation level 1
<2> Indentation level 2
<3> Indentation level 3

**There are a number of inconveniences with this code:**
* Every level of nesting adds a new closure (variables in the outer functions cannot be cleaned up until the entire sequence is completed).
* It is very difficult to visually parse long nested code
* The nesting leads to code that stretches horizontally (so that it doesn't fit in the viewport), which makes code review difficult
* Error handling is very manual (you need to remember to handle the errors at each callback)
* Any exceptions thrown in the callback functions become UnhandledExceptions

Consider the following code where we've refactored to use promises:

```javascript
function checkPass(password) {
  return getUserById(id)
    .then(user => compareUserPassword(user.password, password))
    .then(getFilteredProps);
}

// and to call it
checkPass(req.password)
  .then(userProps => resp.json(userProps))
  .catch(err => resp.sendError('password check failed'));
```

**Some benefits gained**
* Improved readability (fewer levels of indentation, concise functions)
* Error handling is propagated and can be handled in a single place
* Exceptions thrown can be caught in the promise chain and won't result in UnhandledExceptions
