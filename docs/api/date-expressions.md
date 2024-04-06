# API Endpoints: Query string date expressions

Date expressions can be used in the `query` parameter when retreiving and filtering Requests from the API.

The expression starts with an anchor date, which can either be `now` (or `*`), or a date string ending with `||` (two pipe characters).

This anchor date can optionally be followed by one or more maths expressions:

* `+1h` – Add one hour
* `-1d` – Subtract one day
* `/d` – Round down to the nearest day


The supported time units differ from those supported by time units for durations. The supported units are:

| Symbol | Meaning |
|--------|---------|
| y      | Years   |
| M      | Months  |
| w      | Weeks   |
| d      | Days    |
| h      | Hours   |
| H      | Hours   |
| m      | Minutes |
| s      | Seconds |

Assuming now is 2001-01-01 12:00:00, some examples are:

| Example             | Resolves to                                                                                     |
|-|-|
| now+1h              | now in milliseconds plus one hour. Resolves to: 2001-01-01 13:00:00                             |
| now-1h              | now in milliseconds minus one hour. Resolves to: 2001-01-01 11:00:00                            |
| now-1h/d            | now in milliseconds minus one hour, rounded down to UTC 00:00. Resolves to: 2001-01-01 00:00:00 |
| 2001.02.01\|\|+1M/d | 2001-02-01 in milliseconds plus one month. Resolves to: 2001-03-01 00:00:00                     |