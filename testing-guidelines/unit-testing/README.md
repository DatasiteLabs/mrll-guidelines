## Unit Tests

When to choose Unit Testing?

----

Unit tests checks one thing at a time, tests should not care about the points of interaction between different units of the application.

Unit tests can also be divided into 2 categories:

1. **Isolated**: when we just test component functions.
2. **Shallow**: testing components template without rendering its children. Named "shallow", because they reduce the visual surface of the component to just those elements in the component's template that matter for tests.

> In the shallow test we mock up every single dependency of a component, and we do not render any of the component’s children. The goal is to exercise one slice of the component tree in isolation.

####  Deep Dive

* [Setup](setup.md): How to set up unit tests
* [Examples](examples.md): Here are some use case examples for unit testing
* [What to Avoid](what-to-avoid.md): Checklist of things to avoid in a unit test

#### Difference between Integration Tests

Integration tests are more complicated to set-up and runs slower. Developers end up writing more Integration tests because of a  common misconception: if you are not testing with the real setup of your component, injecting real services and including all of the child components, you are not really testing the component/service. 

If you have a good separation of dumb/smart components, have common libraries for reusable functionality and components, it will be easier to know when and where to use Unit tests vs Integration Tests. 

> Common components and Services need to have Unit tests. You do not know where and when the class you are testing will be used. 

This doesn't mean you do not test the common components in an integrated test.

> Write Integration Tests for your Common classes in  the module you use them to see how they are working in your application.  

