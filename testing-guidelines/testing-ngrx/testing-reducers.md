## Testing NgRx Reducers

### Background

NgRx reducers manage state changes based on processing actions. 

NgRx reducers are pure functions. With the same input *state* and *action*, pure reducer functions should always output the same resultant *state*.

### Testing Philosophy
 
To test Reducers, developers simply mock store state (or use `initialState`), import the *reducerFunction*
and then call the reducerFunction() with mock store state and specific action instances. The reducer will return either the same state or new state.
> Reducers should never mutate properties inside the same state object.
 
Understanding this process allows developers to easily verify state changes for a specific action!

<br/>

----

<br/>



#### Preparing test Test Shell

Here is a **Reducer** test shell based on actual code snippets from the VNDX `project.reducer.ts`:

```ts
import { buildProjectItems } from './testing/project-item.mock';

import {
  ProjectItemsLoaded,
  SearchByCriteria
} from './project.actions';
import { getProjectInitialState, projectReducer, DEFAULT_SEARCH } from './project.reducer';
import { ProjectState } from './project.interfaces';

describe('Project Reducer', () => {
  let initialState;
  beforeEach(() => {
    initialState = getProjectInitialState();
  });

});
 
```

The `beforeEach` always builds a new version of default `ProjectState` using:

```ts
export const adapter: EntityAdapter<ProjectItem> = createEntityAdapter<ProjectItem>({
  selectId: (item: ProjectItem) => item.id,
  sortComparer: false
});
export const DEFAULT_SEARCH: SearchCriteria = {
  projectId: '',
  role: ''
};

export function getProjectInitialState(): ProjectState {
  return adapter.getInitialState({
    searchCriteria: DEFAULT_SEARCH,
    filterCriteria: DEFAULT_FILTERS,
    paginator: DEFAULT_PAGINATION,
    sortBy: null,
    selectedIds: [],
    isLoading: false,
    loaded: false,
    error: null
  });
}
``` 
>  Note that above we are using the `@ngrx/entity` **Adapter**, but that is not a requirement.

We also prepare factory functions to build our mock data:

```ts
import { ProjectItem } from '../project.interfaces';

const FILE_TYPES = ['zip', 'png', 'pdf', 'jpeg'];

/**
 * Factory to build 'n' ProjectItem instance
 */
export function buildProjectItems(count = 3): ProjectItem[] {
  return new Array(count).fill(null).map((_, index) => makeProjectItem(index + 1));
}

export function makeProjectItem(id: number): ProjectItem {
  return {
    id: String(id),
    index: '6',
    openViewerLink: false,
    openDownloadLink: false,
    read: false,
    typeClass: 'fileroom',
    typeIconClass: 'icon fa fa-archive',
    spacerWidth: 26,
    name: 'NewFileRoom',
    printIconClass: 'icon icon-permission fa fa-print',
    downloadIconClass: 'icon icon-permission fa fa-cloud-download',
    manageIconClass: 'icon icon-permission fa fa-cogs',
    fileType: FILE_TYPES[id % FILE_TYPES.length],
    availableDate: '2018-04-03T03:13:37.315Z'
  };
}
```

<br/>

----

<br/>

#### Implement Tests 

The primary focus on tests is to validate the reducer processes known actions in expected fashion.

```ts
describe('valid project actions ', () => {
  it('should return set the list of known ProjectItems', () => {
    const list = buildProjectItems(3);    // mock project items
    const action = new ProjectItemsLoaded(list);
    
    const state: ProjectState = projectReducer(initialState, action);

    expect(state.loaded).toBe(true);
    expect(state.error).toBeNull();
    expect(state.isLoading).toBe(false);
    expect(state.paginator.rawList.length).toBe(3);
  });
});
```
> Notice how we use nested `describe()` blocks to group related individual tests (`it(...)`) by context

Our tests, however, should not only validate data changes (based on processed action). Tests should validate that no extra data changes occur to the state.

Since all reducers are called for all actions, our Reducer should always test for unknown actions. 
> Unknown actions should be ignored AND the state output should match the state input.

```ts
describe('unknown action', () => {
  it('should return the initial state', () => {
    const action = {} as any; // tslint:disable-line:no-any
    const state = projectReducer(initialState, action);

    expect(state).toBe(initialState);
  });
});
```

### Full examples

For full detailed example on how to test Reducers, see:

* [VNDX Feature-Project](https://github.com/MerrillCorporation/poc-vindex/blob/d156d0f5403fc17aae10645e343f6ade643a39d1/libs/vndx/feature-project/src/lib/%2Bstate/project.reducer.spec.ts)
