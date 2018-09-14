## Testing NgRx Selectors

### Background

NgRx selectors are essentially queries to access specific portions of our custom state. 


### Testing Philosophy
 
To test Selectors, we mock store state (or use `initialState`), import the queries (aka selectors), and call the query with the mock store state. The query output should return the data expected.
> This allows us to verify query results for specific store state!

The beauty of this testing approach is the following artifacts **are not needed**:

- no Reducers
- no Effects
- no Facades
- no Actions
 
<br/>

----

<br/>

#### Preparing test Test Shell

When testing Selectors, queries expect the ENTIRE store state... not just the feature state! 


So the first part of any test preparation is to build a full-store mock state (aka mock store). 
The `beforeEach` always builds a new version of a mock store .

To easily construct a mock store, we implement factory functions to build our mock data:

```ts
import { ProjectItem } from '../project.interfaces';

const FILE_TYPES = ['zip', 'png', 'pdf', 'jpeg'];

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

We will also prepare another helper function to easily modify our store state:

```ts
/**
 * Update ProjectState field and preserve immutability for ProjectState
 * so memoized selectors fire properly...
 */
function updateProjectState(appState, key, value) {
  const storeState = { ...appState };
  storeState[PROJECT_FEATURE] = { ...appState[PROJECT_FEATURE] };
  storeState[PROJECT_FEATURE][key] = value;

  return storeState;
}
```

Here is a **Selector** test shell based on actual code snippets from the VNDX `project.selectors.ts`:

```ts
import { ProjectState, ProjectItem, SearchCriteria } from './project.interfaces';
import { DEFAULT_SEARCH, getProjectInitialState, adapter } from './project.reducer';
import { projectQuerys, PROJECT_FEATURE } from './project.selectors';
import { makeProjectItem } from './testing/project-item.mock';

describe('ProjectItems Selectors', () => {
  let storeState: { [key: string]: ProjectState };
  let items;

  const getItemId = (it: ProjectItem) => it.id;

  beforeEach(() => {
    items = [33, 45, 67].map(id => makeProjectItem(id));
    storeState = {
      [PROJECT_FEATURE]: <ProjectState> adapter.addAll(items, {
        ...getProjectInitialState(),
        searchCriteria: {
          projectId: '37',
          role: 'admin'
        },
        selectedIds: [],
        loaded: true
      })
    };
  });
  
});
```

By default we populate our state with three (3) mock ProjectItems.

>  Note that above we are using the `@ngrx/entity` **Adapter**, but that is not a requirement.


<br/>

----

<br/>

#### Implement Tests 

The primary focus on tests is to confirm the query outputs expected data known to be in the store state.

```ts
  /**
   * Query for all items and selected items
   */
  describe('item query', () => {
    it('getAllProjectItems() should return the list of ProjectItems', () => {
      const results = projectQuerys.getAllProjectItems(storeState);
      expect(results.length).toBe(3);
    });

    it('getSelectedItems() should return the selected project items', () => {
      let actualId, expectedId, selectedItems;

      expectedId = getItemId(items[1]);
      state = updateProjectState(storeState, 'selectedIds', [expectedId]);
      selectedItems = projectQuerys.getSelectedItems(state);
      actualId = selectedItems.map(getItemId)[0];

      expect(selectedItems.length).toEqual(1);
      expect(expectedId).toBe(actualId);

      expectedId = getItemId(items[2]);
      state = updateProjectState(state, 'selectedIds', [expectedId]);
      actualId = projectQuerys.getSelectedItems(state).map(getItemId)[0];

      expect(expectedId).toBe(actualId);
    });
  });
  
  /**
   * Validate search criteria changes on query results
   */
  describe('searching', function() {

    it('getSearchCriteria() should access search criteria', function() {
      ....  
    });
    
  });
```
> Notice how we use nested `describe()` blocks to group related individual tests (`it(...)`) by context


### Full examples

For full detailed example on how to test Selectors, see:

* [VNDX Feature-Project](https://github.com/MerrillCorporation/poc-vindex/blob/d156d0f5403fc17aae10645e343f6ade643a39d1/libs/vndx/feature-project/src/lib/%2Bstate/project.selectors.spec.ts)
