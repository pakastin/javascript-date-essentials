# JavaScript Date Essentials
Learn how to use JavaScript's Date effenciently

## Basics

### Date object
To create a Date, just call `new Date()`:
```js
const date = new Date();

date // Fri Nov 24 2017 01:22:35 GMT+0200 (EET)
```

You can provide many different formats, for example:
```js
new Date('2017-11-24'); // Fri Nov 24 2017 02:00:00 GMT+0200 (EET)
new Date(1511481600000); // Fri Nov 24 2017 02:00:00 GMT+0200 (EET)
new Date('Fri Nov 24 2017 02:00:00 GMT+0200 (EET)'); // Fri Nov 24 2017 02:00:00 GMT+0200 (EET)
```

### Getting UNIX time
UNIX time means milliseconds since 1.1.1970 00:00:00 UTC

You can get UNIX time now by using `Date.now()` or `date.getTime()`.

```js
Date.now(); // 1511479652772

const date = new Date();
date.getTime(); // 1511479675459
```

We can validate this by creating a new Date with a UNIX time zero:
```js
const zeroDate = new Date(0);

zeroDate // Thu Jan 01 1970 02:00:00 GMT+0200 (EET)
zeroDate.getTime() // 0
```

We get this in local time, so it's not necessarily by midnight, but in UTC it would be 00:00:00.

### Let's build a clock
Well, not a graphical clock, but a CLI clock.

How can we count time to the next full second? Modulo is quite useful here:

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

// tick
// tick
// tick
// ...
```
Watch your computer's clock and see how precise our clock is. Compare it to the usual one:
```js
setInterval(() => {
  console.log('tick', Date.now());
}, 1000);
```

See the difference there?

### Schedule
What if we'd like to schedule some action to precisely the next minute. Let's see:

```js
const MINUTE = 60 * 1000;
const now = Date.now();
const nextMinute = MINUTE - (now % MINUTE);

setTimeout(() => console.log('MINUTE'), nextMinute);
```

## work in progress...
