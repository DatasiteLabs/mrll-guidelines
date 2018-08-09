## Testing

------
- [ ] **Use Jest**
------

### frameworks
There are two main testing frameworks in node: `Jest` and `Mocha`.

#### Mocha
Mocha has been around for a long time and has a number of helpers (`chai` for more readable syntax, `chai-as-promised` for handling asynchronous code. etc.). Mocha needs a test runner to run.

#### Jest
Jest is fairly new but has a number of benefits. It can handle most things out of the box: assertions, spies, mocks, it includes a runner, and many other utilities.

|                         | Mocha                                                                                                                                                                                                                     | Jest                                                                                                                                         | Verdict |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| Out of the box features | Mocha provides only the testing framework. You still need to wire it up with a test runner, assertion library (like Chai and chai-as-promised), mocking library (like Sinon), code coverage library (like Istanbul), etc. | Jest comes with all of those built-in out of the box.                                                                                        | Jest    |
| Configuration           | Mocha needs a fair bit of configuration to set up; you also need to set up the test runner, code coverage tool, etc.                                                                                                      | The configuration is minimal and the framework makes some sensible assumptions to get started quickly (e.g. that test files end in `spec.js` | Jest    |
| Extensibility           | Mocha is a mature framework and has a large community with many extensions                                                                                                                                                | Jest is fairly new and there are extensions for some functions (e.g. typescript support) but not as much as mocha                            | Mocha   |
| Maturity                | Mocha has been around for a long time and some of the associated tooling (e.g. Chai) have been around almost as long                                                                                                      | Jest is fairly new but has a large backing and has the advantage                                                                             | Mocha   |

> Despite being relatively new Jest has the advantage of coming with almost everything needed out of the box. This reduces the amount of setup and configuration required and allows the developer to get started quickly.

**Jest is recommended**
