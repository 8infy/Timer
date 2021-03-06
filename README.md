# Timer | [![Build status](https://ci.appveyor.com/api/projects/status/lq05xlr0cdkk4d5a?svg=true)](https://ci.appveyor.com/project/8infy/timer) | [![Codacy Badge](https://api.codacy.com/project/badge/Grade/114f8af31d8c4ed88a13f9cdbcdb1c96)](https://www.codacy.com/app/8infy/Timer?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=8infy/Timer&amp;utm_campaign=Badge_Grade) |
A simple header-only C++ timer for measuring the performance of your application.

Observational error: ~100 nanoseconds in release with optimizations/inlining enabled.

## Using the timer
### - Create an instance of Timer by calling one of the constructors
-   `Timer()` -> Sets the timer name to `"Unnamed"` and the unit of time to `AUTO`. Result is printed upon destructor call.
-   `Timer(TimeUnit unit)` -> Sets the timer name to `"Unnamed"` and the unit of time to `unit`. Result is printed upon destructor call.
-   `Timer(const char* name)` -> Sets the timer name to `name` and the unit of time to `AUTO`. Result is printed upon destructor call.
-   `Timer(const char* name, bool scoped)` -> Sets the timer name to `name` and the unit of time to `AUTO`. Result is printed upon destructor call if `scoped` was set to `true`.
-   `Timer(const char* name, TimeUnit unit)` -> Sets the timer name to `name` and the unit of time to `unit`. Result is printed upon destructor call.
-   `Timer(const char* name, TimeUnit unit, bool scoped)` -> Sets the timer name to `name` and the unit of time to `unit`. Result is printed upon destructor call if `scoped` was set to `true`.
---
### - Getting your result
-   `void Reset()` -> Resets the timer but does not return nor print the result.
-   `void PrintElapsedReset()` -> Logs the elapsed time to the console and resets the timer.
-   `void PrintElapsed()` -> Logs the elapsed time to the console but does not reset the timer.
-   `double GetElapsedReset()` -> Resets the timer and returns the elapsed time.
-   `double GetElapsed()` -> Returns the elapsed time but does not reset the timer.
-   `~Timer()` -> same as `PrintElapsed()` unless `scoped` was set to `false`.
---
### - Other functions
-   `void SetTimeUnit(TimeUnit unit)` -> Sets the unit of time to `unit`.
-   `ostream& operator<<` -> Allows to use any `Timer` object with streams like `cout`, e.g `std::cout << myTimer`. Same as `GetElapsed()`.
---
### - There is a total of 6 available units of time that reside inside the scoped TimeUnit enum
-   `AUTO`
-   `NANOSECONDS`
-   `MICROSECONDS`
-   `MILLISECONDS`
-   `SECONDS`
-   `MINUTES`

The `AUTO` time unit is meant to be used with `PrintElapsed()` and `PrintElapsedReset()` as it converts the elapsed time into the most convenient unit of time depending on the result. If the time unit is set to `AUTO`, the `GetElapsed()` and `GetElapsedReset()` member functions will return the elapsed time in milliseconds. You can change this behavior by setting the `DEFAULT_AUTO_UNIT_GETTER_` define to the desired unit of time.

The timer automatically converts elapsed time into selected unit of time whenever neccessary.
