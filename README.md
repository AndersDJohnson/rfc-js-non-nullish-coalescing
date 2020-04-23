# rfc-js-non-nullish-coalescing
> A proposal a new JS operator to shorted ternary expressions for nullish values.

We have the nullish coalescing operator as a shorthand ternary to default to some expression when a value is `undefined` or `null` ("nullish"):

```js
const a = b ?? c;
```

But sometimes we want to use a value only if it's not nullish, otherwise we prefer not to use it.

Today we can use verbose ternaries:

```js
const a = b == null ? b : helper(b);
```

But a new non-nullish coalescing operator could make this easier:

```js
const a = b ?? helper(b);
```

So that `helper(b)` (which may require a non-nullish argument in TypeScript) will only be called if `b` is non-nullish.
