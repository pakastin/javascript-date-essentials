# Calendar

## Today

First let's create a Date object for today:
```js
const today = new Date();

// reset the date:
today.setHours(0);
today.setMinutes(0);
today.setSeconds(0);
today.setMilliseconds(0);

today // Fri Nov 24 2017 00:00:00 GMT+0200 (EET)
```

## Beginning of the month

Ok, let's then find out the first date of the month:

```js
const beginningOfTheMonth = new Date(today);

beginningOfTheMonth.setDate(1);

beginningOfTheMonth // Wed Nov 01 2017 00:00:00 GMT+0200 (EET)
```

## End of the month

Nice! Let's move forward to the end of the month:

```js
const endOfTheMonth = new Date(beginningOfTheMonth);

// add one month and substract one millisecond:
endOfTheMonth.setMonth(endOfTheMonth.getMonth() + 1);
endOfTheMonth.setMilliseconds(-1);

endOfTheMonth // Thu Nov 30 2017 23:59:59 GMT+0200 (EET)
```

Wow, that's clever! 😀

## work in progress...
