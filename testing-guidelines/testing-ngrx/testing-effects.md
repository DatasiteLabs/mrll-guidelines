## Testing NgRx Effects

### Background

NgRx Effects serve to centralize all asynchronous processing for a NgRx feature. Effects can also be used to switch and broadcast other events.

### Testing Philosophy
 
 
To test Effects, we must employ integration testing techniques.
 
To test Effects, build a test bed to setup Ngrx with effects, reducers, and selectors, and facade. We mock any services used internally in the Effects. 

Then we test in by dispatching store actions that only the @Effect() will handle and subscribe to the effect observable to see if the desired output is emitted.
 
This allows us to verify Effect observables and impacts of actions stream in the pipeline.
 
<br/>

----

<br/>

#### Preparing test Test Shell

When testing Effects, we should mock our full-store Schema:

```ts
interface TestSchema {
  project: ProjectState;
}
```

Testing Effects will implicitly depend on integration and DI for the reducer, services, effects, and selectors. As such, we need setup an Angular **TestBed** to configure our DI requirements:

Here is a **Effects** test shell based on actual code snippets from the VNDX `project.effects.ts`:

```ts
describe('ProjectEffects', () => {
  let effects: ProjectEffects;
  let metadata: EffectsMetadata<ProjectEffects>;
  let store: Store<TestSchema>;
  let rawList;

  beforeEach(() => {
    rawList = buildProjectItems();
    const initialState = getProjectInitialState();

    TestBed.configureTestingModule({
      imports: [
        NxModule.forRoot(),
        StoreModule.forRoot({}),
        EffectsModule.forRoot([]),
        StoreModule.forFeature(PROJECT_FEATURE, projectReducer, { initialState }),
        EffectsModule.forFeature([ProjectEffects])
      ],
      providers: [
        DataPersistence,
        ProjectFacade,
        {
          provide: VndxService,
          useValue: { getViewIndex: (projectId: string, roleId?: string): Observable<ProjectItem[]> => of(rawList) }
        }
      ]
    });

    effects = TestBed.get(ProjectEffects);
    metadata = getEffectsMetadata(effects);
    store = TestBed.get(Store);
  });
  
  describe('xxxx', function() { ... });
  
});
```

With Effects, we do need to build a mock list of data items (e.g. `ProjectItem[]`).  And since our Effect may trigger HTTP Services we need to prepare mock HttpServices; e.g. `VndxService`.
> Note the use of a value object when building a mock VndxService. The value object will publish the `rawList` and our `it(...)` tests can verify the outputs against the same `rawList` data.


<br/>

----

<br/>


#### Implement Tests for @Effect Observables

The focus for these tests is to confirm the Effect observables emit the expected output after a store action is dispatched:  

```ts
/**
 * Testing the @Effect properties
 */
describe('listen for action', () => {
  it('loadProject$ should return list using "ProjectItemsLoaded" action', () => {
    store.dispatch(new LoadProjectItems('someId', 'someRole'));

    effects.loadProject$.subscribe(action => {
      expect(action.type).toBe(ProjectActionTypes.PROJECT_ITEMS_LOADED);
      expect(action.list.length === rawList.length).toBe(true);
    });
  });

  it('searchProject$ should switch to new action "LoadProjectItems"', () => {
    store.dispatch(new SearchByCriteria({ projectId : '5' }));

    effects.searchProject$.subscribe(action => {
      expect(action.type).toBe(ProjectActionTypes.LOAD_PROJECT_ITEMS);
      expect(action.projectId).toBe('5');
    });
  });
});
```


### Full examples

For full detailed example on how to test Effects, see:

* [VNDX Feature-Project](https://github.com/MerrillCorporation/poc-vindex/blob/d156d0f5403fc17aae10645e343f6ade643a39d1/libs/vndx/feature-project/src/lib/%2Bstate/project.effects.spec.ts)
