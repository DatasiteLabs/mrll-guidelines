#### Creating Feature Libraries

Here is a common question: "Should I create a feature Library?".

To answer that question, ask yourself:

* Am I adding a new route?
* Am I adding a new "application screen"?
* Am I working on an app-specific use case?

All (most) feature libraries are app-specific, so you need to select a application grouping directory to put it.

```
      Adding a new route?    Adding a new screen? App-specific Use Case?
          /                       \
         /no                       \ yes
        /                           \
   Don't Create            Is there a feature lib suited for it?
  New Feature Libs        (it doesn't create new RouterModule.forChild)
                                  /       \
                                 /no       \ yes
                                /           \
                          Create a New       Modify an Existing
                          App-Specific Lib      Feature-Specific Lib
```

#### How to create a Feature Library

You can create a new feature library `timesheets` [for the group of `payroll` features] by running:

```console
ng g lib feature-timesheets --lazy --directory=payroll --tags=payroll,feature
```

The lazy-loaded library will be created in the folder `libs/payroll` and configured with all the tags; tags that will be used later to define usage constraints.


