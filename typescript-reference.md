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

## Troubleshooting

### `An index signature parameter type cannot be a union type. Consider using a mapped object type instead`

If you try to create an index signature for an object by defining the type of the `key` of the object and you try to use an `interface`, you may get the above error.

The answer is to use a `type` instead of an `interface`, as [described here](https://github.com/Microsoft/TypeScript/issues/24220#issuecomment-449325451).

```ts
type Foo = 'a' | 'b'
type Bar = { [key in Foo]: any }   // Works
interface Baz { [key in Foo]: any } // Fails
```
