## What to Avoid


### Repeating the Unit Tests in Integration tests?

Consider an example ApiService. 

* It is a simple service that reads from the environment variable
* The service returns a path for a specific Api. 

##### `libs/common/state/src/lib/services/apiservice.ts`

```ts
 get baseAPIURI(): string {
    return this._baseAPIURI;
  }

  getCurrentRoleApi(projectId: string): string {
    return `${
      this._baseAPIURI
    }projects/${projectId}/contentPermissionGroups/current`;
  }
```

There is no need to test it's functionality outside of it's unit tests. When environment and method arguments are the same, ApiService will always produce the same results, (pure function). Anywhere the ApiService is used is not going to effect the results it returns. 

> If your tests files are too long, that is a good sign that either component is too complex, or you might be testing things that can be tested in a unit test. Ex: Manda [content-data-table.component.spec.ts](/apps/manda/src/app/content/content-data-table/content-data-table.component.spec.ts:1978)


### Mocking Data?

In Integration tests we mock up only platform dependencies(location, language, wifi), we use real service APIs for the of the test data.
