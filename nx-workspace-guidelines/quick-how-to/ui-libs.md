#### Creating UI Libraries

Here is another common question: "Should I create a UI Component Library?"

Again, ask yourself:

* Can I extract some of the functionality into components with only inputs and outputs (i.e., dumb components)?

General Rules:

* If this UI component is specific to the application you are working on, add it to a component library in that appropriate directory. 
* If no suitable component library exists, create a new component library in that directory. 
* If this component can be used across applications, add it to a shared library. 
* If it is shared, document it and add more tests.

<br/>

```
    Adding a ui component that depends only on inputs and outputs?
          /                       \
         / no                      \ yes
        /                           \
   Don't Create           Is this component only used with a specific feature-library?
New `ui` Lib                      /    \
                                 /      \ yes
                                /        \ 
                               /       create a `ui` **folder** in the feature libary
                              /             feature/src/lib/ui
                             / 
                      Is this ui component specific to a particular **application**?
                  My component doesn't display any of the entities listed below.
                                  /       \
                                 /no        \ yes
                               /             \
           Is there a ui library          Is there a ui library
              that suited well for it?      that suited well for it?
                 /no       \ yes                    /no       \ yes
                /           \                     /            \
        Create a New    Modify an Existing    Create a New    Modify an Existing
         Shared Lib        Shared Lib        App-Specific Lib  App-Specific Lib
```

<br/>

Look for opportunities to extract dumb components that can be reused in other contexts.  Ask yourself: 
* Can I extract a dumb component that will do most of the displaying? 
* Can it be used elsewhere? 

> Talk to your team leads.

#### How to create a UI Component Library

You may want to create a UI library of presentational, dumb components. 
For example, let's create a new ui library `timesheets` [for the group of `payroll` features]. 

> Since these components will be used by multiple payroll feature libraries, 
we will create a library that will be shared ONLY for payroll features.


```console
ng g lib ui --directory=payroll --tags=payroll,ui
```

The library will be created in the folder `libs/payroll/ui` and configured with all the tags to restrict imports by only **payroll** feature libraries.
