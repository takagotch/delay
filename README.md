### delay
---
https://github.com/sindresorhus/delay

```js
// test/.js
import {serial as test} from 'ava';
import timeSpan from 'time-span';
import inRange from 'in-range';
import currentlyUnhandled from 'currently-unhandled';
import {AbortController} from 'abort-controller';
import m from '.';

const getCurrentlyUnhandled = currentlyUnhandled();

test('return a resolved promise', async t => {
  const end = timeSpan();
  await m(50);
  t.true(inRange(end(), 30, 70), 'is delayed');
});

test('returns a rejected promise', async t => {
  const end = timeSpan();
  await t.throwsAsync(
    m.reject(50, {value: new Error('foo')}),
    'foo'
  );
  t.true(inRange(end(), 30, 70), 'is delayed');
});

test('able to resolve a falsy value', async t => {
  t.is(
    await m(50, {value: 0}),
    0
  );
});

```

```
```

```
```
