#### Is NO_ERROR_SCHEMA bad?

The NO_ERRORS_SCHEMA tells the Angular compiler to ignore unrecognized elements and attributes. It is not good or bad but important to know when to use it. 


```ts
  // Code Example here
```
​
**Pros**: It is a great helper when you need to shallow test a component without worrying about all components that are child of your component that is being tested.
**Cons**: The compiler won't throw an error when it encounters a custom element or attribute. It simply renders them as empty tags and the browser ignores them. If you forget to include a component, or misspelled it, you wouldn't get a warning either but with Typescript, your editor is good at reminding you missing elements.
