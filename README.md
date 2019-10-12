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






















test('can create a new instance with fixed timeout methods', async t => {
  const cleared = [];
  const callbacks = [];
  const custom = m.createWithTimers({
    clearTimeout(handle) {
      cleared.push(handle);
    },
    
    setTimeout(callback, ms) {
      const handle = Symbol('handle');
      callbacks.push({callback, handle, ms});
      return handle;
    }
  });
  
  const first = custom(50, {value: 'first'});
  t.is(callbacks.length, 1);
  t.is(callbacks[0].ms, 50);
  callbacks[0].callback();
  t.is(await first, 'first');
  
  const second = custom.reject(40, {value: 'second'});
  t.is(callback.length, 2);
  t.is(callbacks[1].ms, 40);
  callback[1].callback();
  try {
    await second;
  } catch (error) {
    t.is(error, 'second');
  }
  
  const third = custom(60);
  t.is(callbacks.length, 3);
  t.is(callbacks[2].ms, 60);
  third.clear();
  t.is(cleared.length, 1);
  t.is(cleared[0], callbacks[2].handle);
});
```

```
```

```
```
