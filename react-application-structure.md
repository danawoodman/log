# React Application Structure

A draft proposal for a standard React project structure.

## General Directory Structure


    src/
      components/   <- React components
      controllers/  <- React connected components
      models/       <- Redux/Rematch models
      middleware/   <- Redux middleware
      services/     <- Service helpers
      store/        <- Redux store and helpers
      config/       <- Immutable data


## Component directory/file structure

Components should be within a directory with all associated files living next to them, like so:


    src/
      components/
        Button/
          index.ts           <- Exports component
          Button.tsx         <- Component
          Button.test.tsx    <- Jest test file 
          Button.module.css  <- CSS module
          Button.story.tsx   <- Storybook story

The file name should match the exported component name, e.g. if you have a component called `MyComponent` the file would be at `src/MyComponent/MyComponent.tsx`.

The `index.ts` file in the project just exports whatever components you want to expose, eg:

```ts
export { MyComponent } from './MyComponent'
```

## Named exports

Use named exports rather than `default` so that the component is easier to search for as well as find and replace. Also, this ensures consistent naming throughout the app.

```ts
export function MyComponent() {
  return <h1>Hi!</h1>
}
```

```ts
import { MyComponent } from './MyComponent'
```

If you have two components with the same name, you can import like:


```ts
import { Foo as Bar } from './Foo'
```

## Group complex components

If you have a component that has multiple sub-components that aren’t reusable outside of the component, it is ok to have them live within the folder of the parent component. Nest them like you would under the `components/` directory and keep the main exported component at the root of the folder, like so:


    src/
      components/
        ComplexComponent/
          index.ts
          ComplexComponent.tsx
          ComplexComponent.test.tsx
          ComplexComponent.module.css
          ComplexComponent.story.tsx
          SubComponent/                 <- Nest sub components under main component
            index.ts
            SubComponent.tsx
            SubComponent.test.tsx
            SubComponent.module.css
            SubComponent.story.tsx

Just make sure to have tests/stories for each sub-component as well.
