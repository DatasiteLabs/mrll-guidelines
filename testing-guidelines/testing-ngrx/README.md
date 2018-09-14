## Testing NgRx

Testing NgRx is the most important testing for your Angular applications. 

Why? 

Because NgRx encapsulates all business logic, data processing & caching, server communications, and notifications to UI layers. 
 
* may leverage unit testing, integration test, TestBed testing. 
* independent of UI testing and workflow testing.
* independent of all animation side affects that may be present in the UI components

----

<br/>

####  Deep Dive

NgRx has 5 primary artifacts that we may consider testing: 

* Actions:  (no need to test these)
* Reducers:  requires **unit testing** with mock store and dispatching actions
* Selectors: requires **unit testing** with mock store and querying for data
* Effects: requires **integration testing** with TestBed and Mock services
* Facade: requires **integration testing** with TestBed and Mock services

To see details on how to test each of the NgRx artifacts, click on a link below:  

* [Testing Reducers](testing-reducers.md)
* [Testing Selectors](testing-selectors.md)
* [Testing Effects](testing-effects.md)
* [Testing Facade](testing-facades.md)

