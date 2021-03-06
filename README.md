# rfc-js-non-nullish-coalescing
> A proposal for a new JS operator to guard non-nullish values.

So now we have the nullish coalescing operator as a shorthand ternary to default to some expression when a value is `undefined` or `null` ("nullish"):

```js
const a = b ?? c;
```

## Problem

Sometimes we want to use a value only if it's ***not*** nullish, otherwise we prefer not to use it.

We have the logical assignment proposal but that doesn't work as an expression. https://github.com/tc39/proposal-logical-assignment

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

Now `helper(b)` is only called if `b` is non-nullish, otherwise the value of the expression is just `b` (`null` or `undefined`).

It also works for complex expressions:

```js
const a = compute(b) !? helper(compute(b));
```

(or to avoid computing twice):

```js
const temp = compute(b);
const a = temp !? helper(temp);
```
