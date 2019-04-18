
# Creating a range of numbers in JavaScript

In languages like Ruby, there are often convenience methods to generate an array of numbers to iterate over, often called a range. For example:

```rb
(0..5).map { |x| puts x }
```

JavaScript doesn't have such a method but using more recent version of ES6 you can get close to that behavior:

```js
Array.from(Array(5).keys()) //=> [ 0, 1, 2, 3, 4 ]
```

Or and even cleaner version using [array destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment):

```js
[ ...Array(5).keys() ] //=> [ 0, 1, 2, 3, 4 ]
```

Of course you could also use a library for this instead. Here is [lodash's `_.range`](https://lodash.com/docs/4.16.2#range):

```js
_.range(5) //=> [ 0, 1, 2, 3, 4 ]
```
