---
layout: post
title: "Date Formats"
date: "2017-06-18 10:09:42 -0500"
---
# Date Formats
In the real world, date formats come in many shapes. The two major ones are usually `MM-DD-YYYY` and `DD-MM-YYYY`. (ie `06-18-2017` and `18-06-2017`). But the trouble with these date formats is that they don't sort well alphanumerically.

## DD-MM-YYYY
This is often the most *logical* date format to use, as it puts the numbers in order of significance. Days are short, years are long. But lets take a list of several dates and sort them alphanumerically in this format. Here's what it would look like:
```
05-07-2017
18-06-2017
20-06-2017
25-12-2020
30-12-1917
```
Well, that's definitely not sorted very well. We can see this just in the first two dates, where `05-07-2017` is coming before `18-06-2017`, despite `18-06-2017` coming first in the calendar. This is because the day is listed before the month, so it has more significance in an alphanumerical sorting algorithm.

## MM-DD-YYYY
This is often the common date format to use in the United States, as to why, I am not sure. But if we take a look at what happens when they get sorted alphanumerically, it might turn out closer to what we would expect.
```
06-18-2017
06-20-2017
07-05-2017
12-25-2020
12-30-1917
```
This seems like it sorted much better than before, although there is still a small problem. This is showing that `12-30-1917` is the last date in the list, despite it being first of all of them in the calendar. To fix this issue, we need to use a date format that may seem irregular.

## YYYY-MM-DD
This format is pretty uncommon, although it is the most logical of the three. The year is the most significant number, so it comes first in the format. What happens when this format is used when sorting?
```
1917-12-30
2017-06-18
2017-06-20
2017-07-05
2020-12-25
```
Interesting, they are sorted by when they come in the calendar now! How did this happen? It's because the most significant number comes first, so it has a higher priority in an alphanumerical sorting algorithm.

## Why not use a Custom Sorting Algorithm?
There isn't always control over what sorting algorithm is used. Sometimes it is handled by the browser, by a library, or by a file system. Media files often take the default name of the date they were created. If the file is named with the `YYYY-MM-DD` format, then it will sort well in the file system, with the oldest images appearing first, and the newest ones appearing last. In a sortable table, some browsers or libraries may not give control as to how dates are sorted, and always sort it alphanumerically.

The moral of this really isn't about date formats at all. It's a reminder that there isn't always control over what happens to everything that we write. We can't always expect everything to happen the way we want it to, and we might need to change our code to make sure that it conforms with other libraries. Sorting dates is probably the easiest example, although if anyone else has other examples that they would like to contribute, I'd love to hear!
