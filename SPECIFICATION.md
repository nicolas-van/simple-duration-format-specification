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
12s 342ms 24µs
```

This corresponds to `12.342024` seconds.

## Specification

### Definitions

**second**: A second according to the [SI](https://en.wikipedia.org/wiki/International_System_of_Units). **Representation symbol**: `s`.
**millisecond**: 10e-3 seconds. **Representation symbol**: `ms`.
**microsecond**: 10e-6 seconds. **Representation symbol**: `µs`.
**nanosecond**: 10e-9 seconds. **Representation symbol**: `ns`.
**minute**: 60 seconds. **Representation symbol**: `m`.
**hour**: 60 minutes. **Representation symbol**: `h`.
**day**: 24 hours. **Representation symbol**: `d`.
**year**: A [Julian year](https://en.wikipedia.org/wiki/Julian_year_(astronomy)), which means 365.25 days. **Representation symbol**: `y`.
