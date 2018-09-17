## Testing NgRx Facades

### Background

NgRx Facades provide a *public api* to our view components and UI layer.  


### Testing Philosophy
 
 
To test Facades, we must employ integration testing techniques.
 
To test Facades, build a test bed to setup Ngrx with effects, reducers, and selectors, and facade. We mock any services used internally in the Effects. 

Then we test in two (2) ways:
 
1. Test Facade observable emissions after call Facade public methods
2. Test Facade observable emissions by directly dispatching store actions
    
This approach allows us to verify Facades observables and the associated impacts of method calls on emitted values!
 
<br/>

----

<br/>

#### Preparing test Test Shell

When testing Facades, we should mock our full-store Schema:

```ts
interface TestSchema {
  project: ProjectState;
}
```

Our Facades will trigger Effects which - in turn - may trigger HTTP Services. So we need to prepare mock HttpServices so our Effects will work as expected:

```ts
/**
 * Mock service used internally in project.effects.ts
 */
export class MockVndxService {
  getViewIndex(projectId: string, roleId?: string): Observable<ProjectItem[]> {
    const rawList = buildProjectItems(6).filter(it => {
      return !projectId ? true : it.id === projectId;
    });
    return of(rawList);
  }
}
```

With Facades, we do not need to build a mock Store (or state). 

Testing Facades will implicitly depend on integration and DI for the reducer, services, effects, and selectors. As such, we need setup an Angular **TestBed** to configure our DI requirements:

Here is a **Facade** test shell based on actual code snippets from the VNDX `project.facade.ts`:

```ts
describe('ProjectFacade', () => {
  let facade: ProjectFacade;
  let store: Store<TestSchema>;

  beforeEach(
    async(() => {
      TestBed.configureTestingModule({
        imports: [
          NxModule.forRoot(),
          StoreModule.forRoot({}),
          EffectsModule.forRoot([]),
          StoreModule.forFeature(PROJECT_FEATURE, projectReducer, { initialState: getProjectInitialState() }),
          EffectsModule.forFeature([ProjectEffects])
        ],
        providers: [
          DataPersistence,
          ProjectFacade,
          { provide: VndxService, useClass: MockVndxService }
        ]
      });

      store = TestBed.get(Store);
      store.dispatch(new ProjectItemsLoaded([]));

      facade = TestBed.get(ProjectFacade);
    })
  );
  
  describe('xxxx', function() { ... });
  
});
```

<br/>

----

<br/>


#### Implement Tests for Public Methods

The focus for these tests is to confirm the Facade observables emit the expected output after a facade **public method** has been invoked:  

```ts
/**
 * These tests invoke facade public methods...
 * and watch results using facade observables
 */
describe('public methods', function() {

  it('searchForItems() should emit mocked data via `allItems$`', async done => {
    try {
      let list;

      list = await readFirst<ProjectItem[]>(facade.allItems$);
      expect(list.length).toBe(0);

      facade.searchForItems('4');

      list = await readFirst(facade.allItems$);
      expect(list.length).toBe(1);

      facade.searchForItems('invalid-projectId');

      list = await readFirst(facade.allItems$);
      expect(list.length).toBe(0);

      done();
    } catch (err) {
      done.fail(err);
    }
  });
  
});
```

> It is important to note the use of async/await, try/catch, and `done` within are testing pattern. This allows us to treat asynchronous processing as a synchronous sequence of test steps.


#### Implement Tests for Public Observables 

The focus for these tests is to confirm that **dispatched actions** to the store trigger the Facade observables to emit expected values.

```ts
/**
 * These tests dispatch actions to the store and watch via Facade observables
 */
describe('observable properties', function() {
  /**
   * Dispatch `ProjectLoaded` action to manually submit list for state management
   */
  it('allItems$ should return the loaded list and loaded flag == true', async done => {
    try {
      let list = await readFirst(facade.allItems$);
      expect(list.length).toBe(0);

      store.dispatch(new ProjectItemsLoaded(buildProjectItems(8)));

      list = await readFirst(facade.allItems$);
      expect(list.length).toBe(8);

      done();
    } catch (err) {
      done.fail(err);
    }
  });
});
```



### Full examples

For full detailed example on how to test Facades, see:

* [VNDX Feature-Project](https://github.com/MerrillCorporation/poc-vindex/blob/d156d0f5403fc17aae10645e343f6ade643a39d1/libs/vndx/feature-project/src/lib/%2Bstate/project.facade.spec.ts)
