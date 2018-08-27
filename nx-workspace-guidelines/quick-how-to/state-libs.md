#### Creating State Libraries

Here is another common question: "Should I create a State Library?"

General Questions:

* Do I need to hit another REST endpoint?
* Do I need to get more data form an existing REST endpoint?
* Do I need a different set of NgRx state management files?
* Do I need to gather all my NgRx state files into one (1) library with associated HTTP (or other) services?
* Do I want all models and interfaces related to the NgRx state to co-live in the same library?
* What other libraries will use the library?
* Will multiple applications use this library?


<br/>

```
    Do I need to hit another endpoint? 
    Do I need more data than I currently have?
          /                       \
         / no                      \ yes
        /                           \
   Don't Create             Is the data specific to my application?
New DataAccess Libs      It isn't anything from the list of entities below.
                                  /        \
                                 /no        \ yes
                               /             \
           Is there a data-access library    Is there a data-access library
              that suited well for it?      that suited well for it?
                 /no       \ yes                    /no       \ yes
                /           \                     /            \
        Create a New    Modify an Existing    Create a New      Modify an Existing
         Shared Lib        Shared Lib         App-Specific Lib   App-Specific Lib
```



<br/>

When considering a new `state` collection, first consider just creating it as a directory 
within an existing feature library. Then look for current or future needs to share this collection of features and functionality. 

* Will it be used by other features in the sample application?
* Will it be used/need within other applications?

Proper state management is critical to development success: Talk to your team leads.

> Writing generic state libraries is challenging

#### How to create a `state` Library

Let's create a new `state` library `timesheets` for the group of `payroll` features. 

This state management feature will be used by multiple payroll feature libraries, 
we will create a library that will be shared ONLY for payroll features. 

> Since we will later have another state collection `invoices`, let be specified in our naming and use the naming convention:
* `state-timesheets`
* `state-invoices`

```
ng g lib state-timesheets --directory=payroll
ng g ngrx timesheets --module=libs/payroll/state-timesheets/src/lib/payroll-state-timesheets.module.ts --facade --tags=payroll,state
```

The library will be created in the folder `libs/payroll/state-timesheets` and configured with all the tags to restrict imports 
by only **payroll** feature libraries or other **payroll** state libraries.
