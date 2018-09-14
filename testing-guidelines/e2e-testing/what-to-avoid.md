## What to Avoid

Here is a checklist of things to avoid in a e2e test:

* E2E tests are great for high-level validation of the **entire system**. But they can't give you the comprehensive test coverage that you'd expect from unit tests.
* E2E tests are **difficult to write** and perform poorly compared to unit tests. They **break easily**, often due to changes or misbehavior far removed from the site of breakage.
* E2E tests can't easily reveal how your components behave when things go wrong, such as **missing or bad data, lost connectivity, and remote service failures**.
* E2E tests for apps that update a database, send an invoice, or charge a credit card **require special tricks and back-doors to prevent accidental corruption of remote resources**. It can even be hard to navigate to the component you want to test.
  
