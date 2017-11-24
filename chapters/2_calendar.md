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
const beginningOfMonth = new Date(today);

beginningOfMonth.setDate(1);

beginningOfMonth // Wed Nov 01 2017 00:00:00 GMT+0200 (EET)
```

Nice!

## End of the month

Then we'll move forward to the end of the month:

```js
const endOfMonth = new Date(beginningOfMonth);

// add one month and substract one millisecond:
endOfMonth.setMonth(endOfMonth.getMonth() + 1);
endOfMonth.setMilliseconds(-1);

endOfMonth // Thu Nov 30 2017 23:59:59 GMT+0200 (EET)
```

Wow, that's clever! 😀

## First sunday / monday
Calendar sheet usually start from sunday or monday. How can we figure out which is the first sunday? Easy!

```js
const weekdayOfBeginning = beginningOfMonth.getDay();
const firstSunday = new Date(beginningOfMonth);

firstSunday.setDate(firstSunday.getDate() - weekdayOfBeginning);

firstSunday // Sun Oct 29 2017 00:00:00 GMT+0300 (EEST)
```

## Last saturday
Here we will use similar technique, than with end of month:

```js
const weekdayOfEnd = endOfMonth.getDay();
const lastSaturday = new Date(endOfMonth);

// find out saturday before last day of month and add 7 days:
lastSaturday.setDate(firstSunday.getDate() - weekdayOfEnd);
lastSaturday.setDate(lastSaturday.getDate() + 7);

lastSaturday // Sat Dec 02 2017 23:59:59 GMT+0200 (EET)
```

Great success! 😎

## work in progress...
