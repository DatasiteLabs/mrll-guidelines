## Integration Test Examples

Here are some use case examples for integration testing

----

<br/>


### Testing with NgRx Store

Use the `StoreModule.forRoot` in your **TestBed** configuration when testing components or services that inject Store.

* Reducers process state changes synchronously, so mocking out the Store isn't required.
* Use the `combineReducers` method with the map of feature reducers to compose the State for the test.
* Dispatch actions to load data into the `Store`.


##### `libs/common/state/src/lib/document/document.component.spec.ts`

```ts
import { async, ComponentFixture, TestBed } from '@angular/core/testing';

import { combineReducers, Store, StoreModule } from '@ngrx/store';

import * as fromFeature from '../+state/project.reducer';
import { DocumentComponent } from './document.component';
import { fromProjectActions } from '../+state/project.actions';

describe('DocumentComponent', () => {
  let component: DocumentComponent;
  let fixture: ComponentFixture<DocumentComponent>;
  let store: Store<fromFeature.ProjectState>;

  beforeEach(async(() => {
    TestBed.configureTestingModule({
      imports: [
        StoreModule.forRoot({
          'feature': combineReducers(fromFeature.projectReducer)
        })
      ],
      declarations: [DocumentComponent]
    }).compileComponents();
  }));

  beforeEach(() => {
    store = TestBed.get(Store);

    spyOn(store, 'dispatch').and.callThrough();

    fixture = TestBed.createComponent(DocumentComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it('should dispatch an action to load data when created', () => {
    const action = new fromProjectActions.LoadProject({});

    expect(store.dispatch).toHaveBeenCalledWith(action);
  });
});
```

