## Checklist
Use this checklist to help you when you are starting and interested in using a Nx Workspace.

* [x] Prerequisites to Using Nx Workspaces
  * [x] Using TypeScript
  * [x] Use Angular 6.x
  * [x] Installed Nx 6.2 or higher
    *  [x] Angular 6.x
    *  [x] RxJS 6.x
    *  [x] NgRx 6.x

----

### Workspace Setup

You should be familiar with the features of the Angular CLI: command line tools installed via `npm install @angular/cli`. To check your workspace setup, check your project's use of the Angular CLI and the Nx schematics.

* The **Angular CLI** (v6.x) command-line tools uses a mono-repository workspace structure that supports 
  * multiple apps, and
  * libraries.
  
* The **Nx** tools extend these workspace structures with 
  * schematics, 
  * conventions, 
  * graph visualization tools, and 
  * build tools.
  
    
![nx-library-composition](https://user-images.githubusercontent.com/210413/44004764-e18dc40e-9e1c-11e8-90f7-f26b35a44824.png)    
----

#### Check your Version of Angular and CLI

To check your version on Angular CLI (and perhaps Nx), use a Terminal command from the root of your project. In our case the workspace project is called `stellar`:

```
ng -v
```

You should see a listing with Angular 6.x packages similar to the following:

![stellar-ng-version](https://user-images.githubusercontent.com/210413/44004635-33fb2784-9e1a-11e8-9763-a98a6b0e5539.jpg)

Notice in this case the `@nrwl/schematics` is not listed since the Angular CLI does not know about *extra* schematics. Let's confirm that the Nx schematics are also available:

```console
npm list  @nrwl/schematics --depth=0
``` 

You should see this:

![stellar-nx-version](https://user-images.githubusercontent.com/210413/44004677-26a6752e-9e1b-11e8-8ba0-23f5cb6be4ff.jpg)


If you are not using Angular CLI in your local project, see if you have the `@angular/cli` installed globally:

```console
npm list -g @nrwl/schematics --depth=0
``` 

You may see something like this:

![npm-global-installs](https://user-images.githubusercontent.com/210413/44003770-5b53fb4c-9e0d-11e8-8fc1-21c8194cc9fe.jpg)


For details on how to install or upgrade your Nx Workspace, see the quick links below.

## Quick Links    

* [ ] Read the [Getting Started](getting-started/README.md) Guide to Nx Workspaces
* [ ] [Using the Angular Console](https://blog.nrwl.io/angular-console-the-ui-for-the-angular-cli-a5d0924240b7): UI for the Angular CLI.

* [ ] [Using Nx Workspaces](reference/using-workspace/README.md) in your Project
  * [ ] [Add a Workspace to existing Project](using-workspaces/add-workspace.md)
  * [ ] [Upgrade an Existing Workspace](using-workspaces/upgrade-existing-workspace.md)
