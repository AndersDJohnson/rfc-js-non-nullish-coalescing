# rfc-js-non-nullish-coalescing
> A proposal a new JS operator to shorten ternary expressions for nullish values.

We have the nullish coalescing operator as a shorthand ternary to default to some expression when a value is `undefined` or `null` ("nullish"):

```js
const a = b ?? c;
```

## Problem

Sometimes we want to use a value only if it's ***not*** nullish, otherwise we prefer not to use it.
Say we want to call `helper(b)` (which may require a non-nullish argument in TypeScript) only if `b` is non-nullish.

Today we can use ternaries:

```js
const a = b == null ? b : helper(b);
```

But those are especially verbose if `b` is a complex expression, e.g.:

```js
const a = compute(b) == null ? compute(b) : helper(compute(b));
```

(or to avoid computing twice):

```js
const temp = compute(b);
const a = temp == null ? temp : helper(temp);
```

## Solution

A new non-nullish coalescing operator (`!?` or perhaps `!??`) to guard such calls could make this easier:

```js
const a = b !? helper(b);
```

```js
const a = compute(b) !? helper(compute(b));
```

(or to avoid computing twice):

```js
const temp = compute(b);
const a = temp !? helper(temp);
```
