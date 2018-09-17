## Overview

Many Angular development efforts suffers from good-intentioned testing practices and poor test coverage. 

When the application is small and the tests are fast to run, requiring tests to be added with every PR seems to be a *good rule* to follow. 
As an application features grows and complexity increases, tests quickly become a requirement.

Yet - ironically - many factors contribute to teams side-stepping proper testing.

If development teams do not maintain a clear distinction between unit tests and integration tests, tests then become hard-to-write, hard-to-maintain and also take a long time to run. When most of the tests are integration tests, (testing how everything in a module works together), every little change breaks a lot of unrelated tests that developers have to fix. Adding new tests and running them takes longer and longer. And NgRx testing - which is often considered a black-art and poorly implemented - is actually the most important testing within any application.


Developers should use this guide to clarify the distinction between tests... and explore our test examples to identify templates for their own product testing.

----

 ### Types of Testing 
 
We have 3 main types of testing, Unit, Integration and e2e. C

> Select a link below to dive into details on a specific arena of testing. 

* Unit:  Unit tests are isolated, and, as a result, can be used to drive the design of our components. 
  > Unit testing checks a single functionality or a component of an application. Ex: a utility service functionality. A component with mock service.   
* Integration: Integration tests are only used to check the correctness.
  > Integration testing is a type of testing to check if different pieces of the modules are working together. Ex: services and components working together.
* e2e: End to end tests goal is to simulate what a real user scenario looks like from start to finish.
  > E2e or end-to-end or UI testing is a methodology used totest whether the flow of an application is performing as designed from start to finish.

Another special focus testing area is 

* NgRx: NgRx tests are a combination of unit and integration testing used to test state change management, async processing, and data-change notifications. 

----

### Resources

Here are useful links to recordings, blogs, or presentations on testing:

* [Testing Angular Components (Nrwl Remote Training)](​https://drive.google.com/file/d/1hr8E_ggXmJjlrC3N_LOiCl_X5y7aPhy1/view?ts=5af9d660​)

----

##### Evaluation Questions 

Be sure to review the section: [Evaluation Questions](evaluation-questions.md) to test your understanding of testing guidelines. 

##### FAQs

Here is a collection of common questions and answers regarding testing:

* [Is NO_ERRORS_SCHEMA bad?](faq.md)
