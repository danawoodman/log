# Coding Style & Practicies

## General Practices

* **Optimize for readability**: Code is read much more than it is written so you should always work on writing legible, clear code that will be obvious to others or yourself after not seeing the code for a long time.
* **Focus on clarity**: You should strive for code that is legible and clear. Avoid fancy tricks and obscure (but perhaps elegant) techniques. It is more important to write code that is maintainable for years to come than to save a few lines of code.
  **Document, document, document**: If you're building something besides the most trivial feature, you should document what your code does and how to use it. This includes:

  * Inline comments where a piece of code might not be clear on first reading or where you had to do something to handle an edge case.
  * React components should use `propTypes` and `defaultProps` (see below)
  * Your functions should have clear argument names
  * You should name your variables useful names (eg not `an` but instead `accountName`)

## JavaScript

Unless a client requires another approach, all developers should write using the latest ES6/7 syntax that is in Stage 1 or greater. In certain situations, we will also allow Stage 0 features like decorators as needed. The `.babelrc` file in each project should spell out what features are supported.

### General tips

* Use TypeScript if possible to fix common development issues and make your code more documented
* Use Eslint to check your code
* Use Prettier to format your code
* Keep your readme file up to date as your project evolves
* Alphabetically order imports, key values and variables so it's easier to find what you're looking for
* Use clear variable names (eg `username` not `un`)

### Formatting code

Please see [project-structure.md][project-structure.md] for info on formatting.

### Variable usage

Use variables to make code more clear:

```js
// Not ideal:
if (!request.headers['content-type'].startsWith('application/json')) {
  // stuff...
}

// Better:
const requestNotJSON = !request.headers['content-type'].startsWith(
  'application/json'
)
if (requestNotJSON) {
  // stuff...
}
```

While this is more code, it makes reading the code easier since you don't have to mentally parse the conditional since the variable name clearly explains what it represents.

### Conditionals

Always prefer to return early rather than nesting if statements:

```js
// Bad!
if (foo) {
  if (bar) {
    return 'bar'
  } else {
    return 'not bar'
  }
} else {
  return 'not foo'
}

// Good!
if (!foo) return 'not foo'
if (!bar) return 'not bar'
return 'bar'
```

If a value needs a default, use an `or` operator:

```js
const active = active || false
```

When a conditional is needed to alternate two simple values, use a "ternary" expression:

```js
const label = user.admin ? 'Admin!' : 'Regular user'
```

**Never nest ternary expressions!**:

```js
// THIS IS BAD DON'T DO IT!
const val = x === 0 ? 'none' : 100 > x ? 'a lot' : 'a few'
```

Nested ternaries are very hard to reason about 99% of the time so they should be avoided.

If a simple conditional has a longer body, use a standard `if` statement:

```js
if (loggedIn) {
  console.log('logged in')
  doSomeThing()
} else {
  console.log('not logged in')
  doSomeOtherThing()
}
```

However, if you can, return early like we discuss above.

If a value needs to be set with a short value but there may be more than two potential values, use inline `if` statements as they read cleanly:

```js
let icon
if (success) icon = 'check'
if (loading) icon = 'spinner'
if (error) icon = 'exclamation-point'
```

### Other Notes

Other notes about JavaScript development:

* **Name files in kebab-case**: For example, `admin-dashboard.js` and _not_ `AdminDashboard.js`. This improves legibility and makes completion on the command line a bit easier.
* **One "thing" per file**: With few exceptions, you should have one isolated piece of functionality per file like a utility function, or a React component. The only main exception is when you need a local helper/component that doesn't make sense to break out. If you're building out a large feature, it may make sense to put all related components in a folder to keep things organized.
  * If things start to get more complicated, place the code in a folder and move each unique part of functionality to it's own file and then create an `index.js`/`index.ts` file to hook everything together.
* **camelCase variables and functions**: Follow JavaScript standards and use `camelCase` for all variables. the only exception is using snake_case for `CONSTANT_VARIABLE_NAMES`.

### More JavaScript Resources

* [Modern JavaScript cheat sheet](https://github.com/mbeaudru/modern-js-cheatsheet)

### React

* **Use stateless function components where possible**: They're easier to reason about, are less code, and don't manage their own state (which is a good goal to attain).
* **Always use `propTypes`**: Makes it easy to know what a component expects
  * **Store common props in `prop-types.js`**: Store any commonly used PropType definitions in a central location so they can be reused.
* Use `defaultProps`, if relevant
* **Name with `.jsx` extensions**: This makes it clear if it is a React component as well as allows for better editor integrations and build process tooling.
* **Actions should be passed into components**: Pass in actions as function references to components rather than the components defining the functions. Main exception is when a state management solution isn't being used.
* **Use container components**: Wrap state management and behavior around your stateless components using a container component that is responsible for managing state and defining functionality.

This is an example stateless functional React component, `user-list.jsx`:

```js
import { Person } from './prop-types.js'
import PropTypes from 'prop-types'
import React from 'react'

function UserList({ users }) {
  return (
    <ul>
      {users.map((user, key) => (
        <li key={key}>
          {user.name} - {user.email}
        </li>
      ))}
    </ul>
  )
}

UserList.propTypes = {
  users: PropTypes.arrayOf(Person),
}

UserList.defaultProps = {
  users: [],
}

export default UserList
```

Storing common prop types:

```jsx
// prop-types.js
export const Person = PropTypes.shape({
  name: PropTypes.string.isRequired,
  email: PropTypes.string.isRequired,
  bio: PropTypes.string,
  age: PropTypes.number,
})
```

#### When to Use Component Classes

In general you should strive to use functional stateless components where possible since they are simpler, more legible and easier to reason about. However, sometimes it makes sense to use component classes (eg `class MyComponent extends React.Component`).

The main reason to use component classes is if you need to hook into the lifecycle events (`componentDidMount`, `componentWillUpdate`, etc) or if you need to store some local state that doesn't make sense in a central store like Redux or MobX.

A common use case would be managing form fields, validation and other temporary state that you don't care is shared throughout the application.

## CSS/SCSS/LESS

If a project is using CSS/SCSS/LESS, then also use Prettier for formatting with the same settings.

* Name selectors using snake-case: `.button-primary`
* Focus on using reusable styles as much as possible (eg Euphoria or similar)
* If writing custom CSS, make sure to think through if it can be made reusable.
