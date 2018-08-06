## Project structure

------
- [ ] **Ensure that all filenames are *lower-case***
- [ ] **Ensure that the root index file contains the minimum amount of initialization code and nothing else**
- [ ] **Ensure that you break the application up by *resources***
- [ ] **Ensure that you are using the recommended libraries for each use case**
------

There are some conventions that will ensure that we have a uniform experience across different Express-based apps:

### Lower-case filenames

Certain file systems are case-insensitive and cause many issues with development, since what may work on that computer won't work on other systems. We always want to be deterministic in our builds and so we should ensure that we keep consistent file naming structure.

* Use only lower-case letters
* Separate words using hyphens
* Use dots to separate the file type and extension e.g. `user.service.ts`

### Root `index.ts`
The only work that is done in the root file is to initialize the app and start Express. Initialization will have at least the following steps:

* Create the express app
* Ensure that request handling is configured (JSON support with `body-parser`, CORS with `cors`)
* Ensure that `helmet` is used
* Register all the routers for each resource
* Retrieve the environment config
* Initialize logging
* Initialize any external connections
* Start listening to the port


> * **Ensure that the root index file contains no more than the bare minimum of initialization logic**
> * **Ensure that you export the initialization promise for the Express app so that you can test the server**
> * **Ensure that initialization is deterministic and that the server does not start unless all the initializations complete successfully**

### Resources

An Express application is easier to reason about and to develop for when it is broken up by resource. All the files related to the concept of a `User` should exist together in a library. This includes the following:

* Router for that resource
** Route handlers for the resource
* A service for that resource

For example, a sample User resource might have the following structure:
```
  libs
  |-- myApp
      |--user
        |--src
            |--lib
            |  |--user.routes.ts
            |  |--user.service.spec.ts
            |  |--user.service.ts
            |  |--user.utils.spec.ts <1>
            |  |--user.utils.ts <1>
            |
            |--index.ts <2>
```
<1> Optional
<2> The barrel exports the router and the service; and everything from utils if it exists


### Libs
Libraries help in modularizing and sharing code. Traditionally enterprises create a private npm repository that would be used to publish packages internally. In a mono-repo setting this is still possible but the intent is to directly use these libraries in our code without publishing them, and then having to import them back into the application.

A back-end application can generally be broken up into smaller single-responsibility libraries that can be composed as needed. Each library is a self-contained module but can also expose services that can handle functionality specific to its particular domain.

.An example of breaking an app into modules
Let's consider a todo list application. The below might be a potential structure for this application.
```
--apps
  |-- todo-app

--libs
  |-- user
  |   |-- index.ts
  |   |-- user.routes.ts
  |   |-- user.service.ts
  |   |-- user.types.ts
  |-- task
  |   |-- index.ts
  |   |-- task.routes.ts
  |   |-- task.service.ts
  |   |-- task.types.ts
  |-- util
      |-- config.service.ts
      |-- log.service.ts
```

Note the library breakdown by domain: if Task needs User, there is a direct dependency. There may be instances where there might be a circular dependency
