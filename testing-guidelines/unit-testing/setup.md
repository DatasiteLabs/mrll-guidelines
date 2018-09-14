### How to Setup Uni Tests

You can create unit tests using only karma setup, like any other JavaScript testing or you can use Angular Testing Suites help.

You can create one (1) describe for the unit tests and one (1) for the integration tests in the same `<xxx>.spec.ts` file. 

##### dashboard.component.spec.ts

```ts
describe('DashboardComponent (integration)', () => {
  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [ DashboardModule ]
    });
  });
  
 it('should...', ()=> {...})
​
});
​
describe('DashboardComponent (unit)', () => {
  beforeEach(() => {
    TestBed.configureTestingModule({
      declarations: [ DashboardComponent ],
      schemas:      [NO_ERRORS_SCHEMA]
    });
  });
​
  it('should...', ()=> {...})
});
```

* Create one describe for every function that has to be unit tested.
* Start the title of every test scenario with “should” to describe the expected behavior.

##### content.service.spec.ts

```ts
describe('ContentService', () => {
  ...
  describe('create content', () => {
​
    it('should create content for files with correct payload',()=> {...})  
  }
  
   describe('when viewing INDEX', () => {
     it('..', ()=> {...})
   }
});
```

Every “describe” function is a test suite and every “it” is a test scenario. 

When we have more than one (1):

##### libs/commont/state/src/lib/services/auth.service.spec.ts

```ts
import { inject, TestBed } from '@angular/core/testing';
...
​
describe('AuthService', () => {
  beforeEach(() => {
    TestBed.configureTestingModule({
      providers: [AuthService, ApiService]
    });
  });
​
  it('should be created', inject([AuthService], (service: AuthService) => {
    expect(service).toBeTruthy();
  }));
});
```
