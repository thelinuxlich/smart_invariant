# smart_invariant

Like `invariant` and `tiny-invariant`, but smarter.

Differences from both

- Although it's called `smart_invariant`, we suggest you import it as `assert`, because it's shorter and more readable
- No prefix
- No dependency on `process.env.NODE_ENV`, the message will be sent whether NODE_ENV is production or not
- No bundling shenanigans (removing the asserts in production, quite the contrary, we WANT to assert!)
- Message is required and must be a string
- Accepts a optional third argument, which is a function that will be called if the invariant fails (be aware that this function won't be try-catched inside smart_invariant, you'd do it yourself in the function body). Example: console.log or log to Sentry

## Usage

```ts
import assert from 'smart_invariant';

assert(1 === 1, '1 is not equal to 1'); // No error
assert(1 === 2, '1 is not equal to 2', () => {
  Sentry.captureMessage('1 is not equal to 2');
}); // Error: 1 is not equal to 2 and Sentry will be notified
```
