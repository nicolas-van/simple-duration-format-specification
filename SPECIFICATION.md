# Simple Duration Format Specification 1.0

## Introduction

### Rationale

This format aims to define a standardized way to represent an amount of time (which means a number of seconds according to the [SI](https://en.wikipedia.org/wiki/International_System_of_Units)) in a human-readable way.

It is not competing with the [ISO 8601 Duration format](https://en.wikipedia.org/wiki/ISO_8601) as that specification allows to represent context-dependant durations, like civil years or months. The Simple Duration Format only uses the SI second as base unit.

There has already been a number of software implementations allowing similar conversion. But most of them do not rely on a strict specification explaining how the format works. This specification aims to correct this aspect.

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
12s 342ms
```

This corresponds to `12.342` seconds.
