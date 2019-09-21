# Typescript Reference

## Language Reference

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

### Getting the type from an object's keys

```ts
const obj = { a: 1, b: 2, c: 3 }
type ServiceKey = keyof typeof obj
// ServiceKey = 'a' | 'b' | 'c'
```

### Using React `useRef()` hook with Typescript

To use the `useRef` hook, make sure to define its return type as `<HTMLInputElement>`.

```ts
function MyComponent() {
  const input = useRef<HTMLInputElement>(null)
  
  return (
    <form 
      onSubmit={e => {
        e.preventDefault()
        alert('Value: ' + input.current.value)
      }}
    >
      <input ref={input} />
    </form>
  )
}
```

### [Generics](https://www.typescriptlang.org/docs/handbook/generics.html)

```ts
interface Lengthwise {
  length: number;
}

function loggingIdentity<T extends Lengthwise>(arg: T): T {
  console.log(arg.length);  // Now we know it has a .length property, so no more error
  return arg;
}
```

```ts
function getProperty<T, K extends keyof T>(obj: T, key: K) {
  return obj[key];
}

let x = { a: 1, b: 2, c: 3, d: 4 };

getProperty(x, "a"); // okay
getProperty(x, "m"); // error: Argument of type 'm' isn't assignable to 'a' | 'b' | 'c' | 'd'.
```

### [Type Guards](https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-guards-and-differentiating-types)

```ts
function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}

if (isFish(pet)) {
  pet.swim();
}
else {
  pet.fly();
}

function move(pet: Fish | Bird) {
  if ("swim" in pet) {
      return pet.swim();
  }
  return pet.fly();
}
```

```ts
function padLeft(value: string, padding: string | number) {
  if (typeof padding === "number") {
    return Array(padding + 1).join(" ") + value;
  }
  if (typeof padding === "string") {
    return padding + value;
  }
  throw new Error(`Expected string or number, got '${padding}'.`);
}
```

## Troubleshooting Typescript

### `An index signature parameter type cannot be a union type. Consider using a mapped object type instead`

If you try to create an index signature for an object by defining the type of the `key` of the object and you try to use an `interface`, you may get the above error.

The answer is to use a `type` instead of an `interface`, as [described here](https://github.com/Microsoft/TypeScript/issues/24220#issuecomment-449325451).

```ts
type Foo = 'a' | 'b'
type Bar = { [key in Foo]: any }   // Works
interface Baz { [key in Foo]: any } // Fails
```

## External resources

- [The Do's and Don'ts of Typescript](https://www.typescriptlang.org/docs/handbook/declaration-files/do-s-and-don-ts.html)
