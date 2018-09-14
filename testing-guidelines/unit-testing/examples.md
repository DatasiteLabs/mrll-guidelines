## Unit Test Examples

Here are some use case examples for unit testing

----

<br/>


### Testing Services (no dependencies)

Typically developers configure the Angular testing suite `TestBed` to prepare injected services and configure module dependencies.

##### `libs/common/state/src/lib/services/config.service.spec.ts`

```ts
beforeEach(() => {
  TestBed.configureTestingModule({
    providers: [ConfigService]
  });
});
```

We can, however, test unit test services without using any help of the Angular testing suite.

> AngularCLI automatically include TestBed and configure TestingModule but you can test some Services without it.

Once you're strong enough, save the world:

##### `libs/common/state/src/lib/services/config.service.spec.ts`

```ts
import { ConfigService } from './config.service';

describe('ConfigService', () => {
  let service: ConfigService;
  beforeEach(() => { service = new ConfigService(); });

  it('should be created',() => {
    expect(service).toBeTruthy();
  });

  it('should return vndx config',
    () => {
      const vndxConfig = {
        apiURI: '/api/'
      };

      expect(service.getVndxConfig()).toEqual(vndxConfig);
    }
  );
});

```

Below test is accomplishing the same result with using angular testing modules inject method. 
> Still no need for TestBed to be configured.

##### `libs/common/state/src/lib/services/config.service.spec.ts`

```ts
import { inject } from '@angular/core/testing';

import { ConfigService } from './config.service';

describe('ConfigService', () => {

  it('should be created', inject([ConfigService], (service: ConfigService) => {
    expect(service).toBeTruthy();
  }));

  it('should return vndx config', inject(
    [ConfigService],
    (service: ConfigService) => {
      const vndxConfig = {
        apiURI: '/api/'
      };

      expect(service.getVndxConfig()).toEqual(vndxConfig);
    }
  ));
});
```

### Testing Services (with dependencies)

Services often depend on other services that Angular injects into the constructor. We can manually inject the dependent service to the service being tested without the help of TestBed.

##### `libs/common/state/src/lib/services/api.service.spec.ts`

```ts
import { ApiService } from './api.service';
import { ConfigService } from './config.service';

describe('ApiService', () => {
  let apiService: ApiService;

  it('should be created', ()=> {
    apiService = new ApiService(new ConfigService());
    expect(apiService.baseAPIURI).toBeTruthy();
  })
  
  it('should return authorization token', () => {
    expect(service.getAuthorizationToken()).toEqual('');
  });
});
```

### When we need the `TestBed`

When we service creation becomes more complicated, we can use the help of `TestBed` instead.

Consider the manual construction of our `AuthService`:

##### `libs/common/state/src/lib/services/auth.service.spec.ts`
```ts
authService = new AuthService(new ApiService(new ConfigService()));
```
When a service has a dependent service, Dependency Injection(DI) finds or creates that dependent service. And if that dependent service has its own dependencies, DI finds-or-creates them as well.

You must at least think about the first level of service dependencies but you can let Angular DI do the service creation and deal with constructor argument order when you use the `TestBed` testing utility to provide and create services.

```ts
import { inject, TestBed } from '@angular/core/testing';

import { ApiService } from './api.service';
import { AuthService } from './auth.service';

describe('AuthService', () => {
  beforeEach(() => {
    TestBed.configureTestingModule({
      providers: [AuthService, ApiService]
    });
  });

  it('should be created', inject([AuthService], (service: AuthService) => {
    expect(service).toBeTruthy();
  }));

  it('should return authorization token', inject(
    [AuthService],
    (service: AuthService) => {
      expect(service.getAuthorizationToken()).toEqual('');
    }
  ));
});
```

----

<br/>

### Shallow Testing


