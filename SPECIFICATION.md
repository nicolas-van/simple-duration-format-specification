# Simple Duration Format Specification Draft

## Introduction

### Rationale

This format aims to define a standardized way to represent an amount of time (which means a number of seconds according to the [SI](https://en.wikipedia.org/wiki/International_System_of_Units)) in a human-readable way.

It is not competing with the [ISO 8601 Duration format](https://en.wikipedia.org/wiki/ISO_8601) as that specification allows to represent context-dependant durations, like civil years or months. The Simple Duration Format only uses the SI second as base unit.

There has already been a number of software implementations allowing similar conversion. But most of them do not rely on a strict specification explaining how the format works, making it impossible to have a proper cross-language support. This specification aims to correct that aspect.

This Simple Duration Format is precise to the nanosecond as it is the most precise time measurement accessible by common means in today's computing.

### Examples

Here are some quick example:

```
25m 12s
```

This corresponds to `312` seconds.

```
1y 45d 6h 25m 12s
```

This corresponds to `35468712` seconds.

```
-12s 342ms 24µs
```

This corresponds to `-12.342024` seconds.

## Specification

### Definitions

* **second**: A second according to the [SI](https://en.wikipedia.org/wiki/International_System_of_Units).

  *Representation symbol*: `s`.

* **millisecond**: 10e-3 seconds.

  *Representation symbol*: `ms`.
  
* **microsecond**: 10e-6 seconds.

  *Representation symbol*: `µs`.
  
* **nanosecond**: 10e-9 seconds.

  *Representation symbol*: `ns`.
  
* **minute**: 60 seconds.

  *Representation symbol*: `m`.
  
* **hour**: 60 minutes.

  *Representation symbol*: `h`.
  
* **day**: 24 hours.

  *Representation symbol*: `d`.
  
* **year**: A [Julian year](https://en.wikipedia.org/wiki/Julian_year_(astronomy)), which means 365.25 days.

  *Representation symbol*: `y`.

### Format

This document will use the regular-expression common format used by many programming language. In case of misunderstanding use the JavaScript regular expression documentation as reference. The `${}` operator is used when referring to another regular expression defined in the document.

```
simple_duration = ${ws}*-?${ws}*${element}+${ws}*
```

```
element = ${years}|${days}|${hours}|${minutes}|${seconds}|${milliseconds}|${microseconds}|${nanoseconds}
```

```
years = ${positive_number}${ws}*y
```

```
days = ${positive_number}${ws}*d
```

```
hours = ${positive_number}${ws}*h
```

```
minutes = ${positive_number}${ws}*m
```

```
seconds = ${positive_number}${ws}*s
```

```
milliseconds = ${positive_number}${ws}*ms
```

```
microseconds = ${positive_number}${ws}*µs
```

```
nanoseconds = ${positive_number}${ws}*ns
```

```
positive_number = (?:0|[1-9]\d*)(?:\.\d+)?
```

```
ws = the space character or the tab (\t character)
```

### Convertions to seconds

Each `element` encountered is multiplied by its corresponding unit and added to a global number of seconds. After this operation the `-` operator should be applied if present.

### Normalization

It should be noted that this format allows expressions like `345h` (specifying more hours that a day can contain), `0.1m` (a fraction of a unit that could be expressed with smaller units), `24m 3m` (specifying the same unit multiple times), `3h 2y 3ms 4d` (using illogical ordering) or `0y 1s` (specifying a useless unit). This is a desirable particularity for easy human writing and ease of software implementation.

When formatting an amount of time to the Simple Duration Format, a software **must** use a normalization process to write the output. The normalization process is as follow:

First write the `-` sign if necessary and consider the absolute value of the amount to convert for the rest of the writing process. Take the most significant unit (the year) and detect if that amount is greater that 0. If that's the case write it to the output. Remove the corresponding amount of seconds and repeat for all following units from the most significant to the least significant (the nanosecond). If at the end no element was written at all write `0s`.

Example of normalization:

* `345h` -> `14d9h`
* `0.1m` -> `6s`
* `24m 3m` -> `27m`
* `3h 2y 3ms 4d` -> `2y 4d 3h 4ms`
* `0y 1s` -> `1s`

### Rounding

Due to hard-to-predict behaviors in float representations, all software implementations **must** provide a rounding mechanism allowing to round the ouput to a given unit while formatting. The default value for that rounding **should** be the millisecond as it is the most common use case due to time representation is most programming languages.
