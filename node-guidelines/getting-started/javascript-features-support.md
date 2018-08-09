### Javascript features support

------
- [ ] **Use typescript**
- [ ] **Remember to import the typings for third-party dependencies and to save them in devDependencies**
- [ ] **Use the same `tslint.json` and `tsconfig.json` whenever possible**
------

#### Typescript
Typescript is used in the front-end with Angular and it makes sense to keep things consistent when writing code with node as well.

A further advantage, though one that is not as important with newer versions of node, is that it shields the developer from trying to account for which features are supported by the underlying node version. Typescript can transpile code to previous versions of the ECMAScript spec so that it can be compatible with older versions of node. Polyfills can be used when needed.

#### Typings
When working with typescript in node, we must remember to install and save the typings for node libraries. A lot of the node libraries are written and/or distributed in pure javascript without typings, and we need to ensure that the typings are present for support in IDEs and editors.

#### Formatting
It is recommended to use Prettier to assist with maintaining consistent formatting of the code and to avoid whitespace changes in diffs.

#### Linting and tsconfig.json
It is recommended that the same `tslint.json` and `tsconfig.json` be used as in the front-end so that developers won't need to re-orient themselves when switching from one to the other. This is easier to accomplish in a mono-repo.

#### Other options
Other options are to use Babel to transpile the code, or to simply write javascript though this will require the developer to know which version of node is being targeted and also to rewrite the code when the node version is changed.
