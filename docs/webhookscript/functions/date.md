# Date and Time Manipulation

### Supported date and time formats

In WebhookScript, dates are not a specific type, but rather expressed as strings that WebhookScript will attempt to parse using a very powerful date parsing engine.

WebhookScript supports a variety of date formats, and functions taking a date will attempt to guess the format of the input string in order to parse the date into a ISO-8601 format

If possible, it's recommended to use the ISO-8601 format, for example `2020-05-27T04:00:00.000000Z`.

* [List of date format characters](/webhookscript/date-format.html) for the `to_date` and `date_format` functions.

* [List of locales/translations available for date display functions](/webhookscript/date-locales.html)

* [List of Timezone names](/webhookscript/date-format.html#timezone-list)

#### Recognized date formats

In addition to automatically recognizing date strings like ISO-8601, WebhookScript has ability to recognize the following special formats.

* `now`
* `+4 day`, `-2 month` - adds or subtracts to the current date and time, can be suffixed to other dates
    * Other units supported: `second`, `minute`, `hour`, `day`, `fortnight`, `week`, `month`, `year`
* `next Thursday`
* `last Monday`
* `first day of January 2008`
* `first Saturday of July 2008`
* `Monday next week`
* `@1215282385` - UNIX timestamp

For more information, [PHP Supported Date and Time Formats](https://www.php.net/manual/en/datetime.formats.php).

### now(***?string*** timezone) : string

Returns the current date in ISO-8601 format, using `timezone`, if specified.

```javascript
now()
// -> 2022-12-15T11:00:00.000000Z

now('America/Los_Angeles')
// -> 2022-12-15T03:00:00.000000-08:00
```

### to_date(***string*** date, ***?string*** input_format, ***?locale*** locale, ***?string*** timezone, ***bool*** keep_timezone = false): ***?string***

Returns a ISO-8601 formatted date string in UTC time from the provided `date` string.

If specified, `input_format` is used to parse the date without having to guess the format (see the [Date Format Characters](/webhookscript/date-format.html) specification.) Otherwise, see [Recognized date formats](#recognized-date-formats). 

If the `keep_timezone` parameter is set to true, the resulting date string will keep the timezone. The `locale` parameter will attempt to parse the date using the specified locale.

If the date is invalid or could not be guessed, `null` is returned.

```javascript
// Current date and time
'now'.to_date()
// -> 2020-11-25T00:00:00.000000Z

// Relative formats
'first monday august 2019'.to_date()

// Automatic format guessing
'2020-01-01 23:02:01'.to_date()

// Timezone handling
'2020-01-01 23:02:01'.to_date(null, null, 'GMT-5')
// -> "2020-01-02T04:02:01.000000Z", interpreted as GMT-5 and converted to UTC

'2020-01-01 23:02:01'.to_date(null, null, 'GMT-5', true)
// -> "2020-01-01T23:02:01.000000-05:00", date keeps timezone

// Unix timestamp
'@1215282385'.to_date()

// Custom date format
'2/4/12 06:03'.to_date('M/D/YY HH:mm')
// -> 2012-02-04T06:03:00.000000Z

// To escape characters in the format string, backslashes can be used
'2020-01-05 12h30m15s'.to_date('YYYY-MM-DD HH\\hmm\\mss\\s')
// -> 2020-01-05T12:30:15.000000Z
```

### date_format(***string*** date, ***?string*** format, ***?string*** locale, ***?string*** timezone): ***string***

Returns a date converted to the format specified in `format`. `date` is automatically parsed and can be a date string (ISO-8601 recommended) or one of the [recognized date formats](#recognized-date-formats).

For a full list of date format characters, see the [Date Format Characters](/webhookscript/date-format.html) specification.

If `format` is not specified, a default human readable readable string is returned.

```javascript
date_format('2008-07-05T18:26:25.000000Z', 'YYYY-MM-DD') 
// -> 2008-07-05

date_format('2008-07-05T18:26:25.000000Z', 'LLLL', 'da') 
// -> lørdag d. 5. juli 2008 kl. 18:26

date_format('2020-01-01T23:02:01.000000-05:00', 'LLLL', null, 'GMT+2') 
// -> Thursday, January 2, 2020 6:02 AM

date_format('now', 'x')
// -> 1606329669220 (current date in UNIX timestamp with microseconds)

// Add 1 hour to an existing date (see Recognized date formats above)
date_format('2021-10-28 11:28:55 +1 hour', 'YYYY-MM-DD HH:mm:ss')
// -> 2021-10-28 12:28:55
```

### date_to_array(***string***): ***array***

Returns an array containing all the components of a given date.

```javascript
dump(date_to_array('2008-07-05T18:26:25.324542Z'))

// [
//   "year": 2008,
//   "month": 7,
//   "day": 5,
//   "dayOfWeek": 6,
//   "dayOfYear": 187,
//   "hour": 18,
//   "minute": 26,
//   "second": 25,
//   "micro": 324542,
//   "timestamp": 1215282385,
//   "formatted": "2008-07-05 18:26:25",
//   "timezone": "Z"
// ]
```

### date_interval(***string*** date1, ***?string*** date2, ***?string*** format): ***string/int***

Calculates the interval between `date1` and `date2`. When `date2` is unspecified/null, `now` is used.

If no format string is specified, the interval is returned as the number of seconds between the dates, with the number being negative if `date2` is before `date1`.

For the `format` string, the [PHP `DateInterval` format specification](https://www.php.net/manual/en/dateinterval.format.php) is used.

```javascript
date_interval('2008-07-16T23:13:26.234212Z', '2008-07-05T18:26:25.324542Z') 
// -> -967620

date_interval(
    '2008-07-16T23:13:26.234212Z',
    '2008-07-05T18:26:25.324542Z',
    '%d days, %h hours, %i minutes'
)
// -> 11 days, 4 hours, 47 minutes
```

### date_interval_human(***string*** date1, ***?string*** date2, ***?string*** locale): ***string/int***

Formats the difference between 2 dates in a way that's easy to read for humans.

If no locale is specified, English is used.  When `date2` is unspecified/null, `now` is used.

```javascript
date_interval_human(
    '2008-07-16T23:13:26.234212Z',
    '2008-07-05T18:26:25.324542Z'
)
// -> 1 week after

date_interval_human(
    '2008-07-16T23:13:26.234212Z',
    '2008-07-05T18:26:25.324542Z',
    'es'
)
// -> 1 semana después
```
