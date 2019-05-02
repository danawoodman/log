# Typescript Reference

### External resources

- [The Do's and Don'ts of Typescript](https://www.typescriptlang.org/docs/handbook/declaration-files/do-s-and-don-ts.html)

### Get the return type of a function

```ts
function foo() {
  return 'bar'
}

type FooReturn = ReturnType<typeof foo>
``` 

### Extend an external module's types

```ts
declare module 'some-module' {
  export interface SomeInterface {
    // We extend SomeInterface from the "some-module" library to
    // add the "newField" property.
    newField?: string
  }
}
```
