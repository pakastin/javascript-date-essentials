# 1. Clock

## Date object
To create a [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date), just call `new Date()`:
```js
const date = new Date();

date // Fri Nov 24 2017 01:22:35 GMT+0200 (EET)
```

Date is mutable. If you want to clone a date, just wrap it with `const clonedDate = new Date(date)`.

You can provide many different formats as well, for example:
```js
new Date('2017-11-24'); // Fri Nov 24 2017 02:00:00 GMT+0200 (EET)
new Date(1511481600000); // Fri Nov 24 2017 02:00:00 GMT+0200 (EET)
new Date(2017, 0, 1); // Sun Jan 01 2017 00:00:00 GMT+0200 (EET) 
new Date('Fri Nov 24 2017 02:00:00 GMT+0200 (EET)'); // Fri Nov 24 2017 02:00:00 GMT+0200 (EET)
```

## Getting UNIX time
[UNIX time](https://en.wikipedia.org/wiki/Unix_time) means milliseconds since 1.1.1970 00:00:00 UTC

You can get UNIX time now by using `Date.now()` or `date.getTime()`.

```js
Date.now(); // 1511479652772

const date = new Date();
date.getTime(); // 1511479675459
```

We can validate this by creating a new Date with a UNIX time zero (midnight at UTC):
```js
const zeroDate = new Date(0);

zeroDate // Thu Jan 01 1970 02:00:00 GMT+0200 (EET)
zeroDate.getTime() // 0
```

## Tick, tick, tick

How can we count time to the next full second? [Modulo](https://en.wikipedia.org/wiki/Modulo_operation) is quite useful here:

```js
Date.now() % 1000 // How many milliseconds since last round second
```

```js
const tick = () => {
  const now = Date.now();
  const nextTick = 1000 - (now % 1000); // How many milliseconds until next round second
  setTimeout(tick, nextTick);

  console.log('tick', Date.now());
};

tick(); // start clock;

// tick 1511652140001
// tick 1511652141001
// tick 1511652142002
// ...
```
Watch your computer's clock and see how precise our "ticker" is. Compare it to the usual one:
```js
setInterval(() => {
  console.log('tick', Date.now());
}, 1000);

// tick 1511652183704
// tick 1511652184705
// tick 1511652185709
// ...

```

See the difference there?

The cool thing about the nextTick trick is, that when your computer's clock synchronizes itself, the function can synchronize as well. Also you never miss a second or hit a second twice, because it's right on time.

## Let's add hours, minutes and seconds

First we need a helper to ensure leading zeros when there's not enough digits:
```js
const ensureDigits = (num, count) => {
  if (count === 2) {
    return ('0' + num).slice(-2); // add leading zero and take two last characters
  } else if (count === 3) {
    return ('00' + num).slice(-3);
  }
};
```

Then we can build the clock:

```js
const tick = () => {
  const date = new Date();
  const now = date.getTime();
  const nextTick = 1000 - (now % 1000); // How many milliseconds until next round second
  setTimeout(tick, nextTick);

  const hours = ensureDigits(date.getHours(), 2);
  const minutes = ensureDigits(date.getMinutes(), 2);
  const seconds = ensureDigits(date.getSeconds(), 2);
  const milliseconds = ensureDigits(date.getMilliseconds(), 3);

  console.log(`${hours}:${minutes}:${seconds}:${milliseconds}`);
};

tick(); // start clock;

// 00:32:34:001
// 00:32:35:001
// 00:32:36:002
// ...
```

Our clock is ~1ms precise, not bad.

## Next chapter

[Chapter 2. Calendar](2_calendar.md)

## work in progress...
