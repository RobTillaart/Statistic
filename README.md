
[![Arduino CI](https://github.com/RobTillaart/Statistic/workflows/Arduino%20CI/badge.svg)](https://github.com/marketplace/actions/arduino_ci)
[![Arduino-lint](https://github.com/RobTillaart/Statistic/actions/workflows/arduino-lint.yml/badge.svg)](https://github.com/RobTillaart/Statistic/actions/workflows/arduino-lint.yml)
[![Arduino-lint](https://github.com/RobTillaart/Statistic/actions/workflows/arduino-lint.yml/badge.svg)](https://github.com/RobTillaart/Statistic/actions/workflows/arduino-lint.yml)
[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/RobTillaart/Statistic/blob/master/LICENSE)
[![GitHub release](https://img.shields.io/github/release/RobTillaart/Statistic.svg?maxAge=3600)](https://github.com/RobTillaart/Statistic/releases)


# Statistic

Header-only statistic library for Arduino includes sum, average, variance and standard deviation.

The `stat::Statistic<T, C, bool _useStdDev>` class template accepts 3 arguments:

* **`typename T`:** The floating point type used to represent the statistics.
* **`typename C`:** The unsigned integer type to store the number of values.
* **`typename _useStdDev`:** Compile-time flag for using variance and standard deviation.

To maintain backwards compatibility with API <= 0.4.4, the `Statistic`
class implementation has been moved to the `stat` namespace and a
`typedef stat::Statistic<float, uint32_t, true> Statistic` type
definition has been created at global scope.

The `useStdDev` boolean was moved from a run-time to a compile-time
option for two reasons.  First, the compile-time option allows the
optimizer to eliminate dead code (calcuating standard deviation and
variances) for a slightly smaller code size.  Second, it was observed
in uses of the library that the `useStdDev` boolean was set once in
the class constructor and was never modified at run-time.

## Description

The statistic library is made to get basic statistical information from a 
one dimensional set of data, e.g. a stream of values of a sensor.

The stability of the formulas is improved by the help of Gil Ross (Thanks!)


## Interface

- **Statistic(void)** Default constructor.
- **void clear()** resets all variables.
- **float add(float value)** (since 0.4.3) returns value actually added to internal sum.
If this is (much) different from what should be added it might become time to call **clear()**.
- **uint32_t count()** returns zero if count == zero (of course).
- **float sum()**      returns zero if count == zero.
- **float minimum()**  returns zero if count == zero.
- **float maximum()**  returns zero if count == zero.
- **float average()**  returns NAN  if count == zero.

These three functions only work if **useStdDev == true**

- **variance()**         returns NAN if count == zero.
- **pop_stdev()**        population stdev, returns NAN if count == zero.
- **unbiased_stdev()**   returns NAN if count == zero.

Deprecated methods:

- **Statistic(bool)** Constructor previously used to enable/disable the standard deviation
functions. This argument now has no effect.  It is recommended to migrate your code to the default constructor (which now also implicitly calls `clear()`).
- **void clear(bool)** resets all variables.  The boolean argument is ignored. It is recommended to migrate your code to `clear()` (with no arguments).

## Operational

See examples.


## Faq

See faq.md


## Future

- update documentation
  - links that explain statistics in more depth
- derived classes
  - 32 bit with fixed sign version? 
  - 64 bit with fixed sign version?
  - double version?
- create releaseNotes.md

