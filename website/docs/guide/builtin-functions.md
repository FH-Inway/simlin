---
id: builtin-functions
title: Builtin Functions
sidebar_label: Builtin Functions
---

# Builtin Functions

Simlin provides a comprehensive set of builtin functions for use in your system dynamics models. These functions are categorized into mathematical functions, time-based functions, test functions, array functions, and standard library functions.

## Mathematical Functions

### Trigonometric Functions

#### `SIN(x)`
Returns the sine of x (where x is in radians).

**Example:** `SIN(3.14159)` ≈ 0

#### `COS(x)`
Returns the cosine of x (where x is in radians).

**Example:** `COS(0)` = 1

#### `TAN(x)`
Returns the tangent of x (where x is in radians).

**Example:** `TAN(0)` = 0

#### `ARCSIN(x)`
Returns the arcsine of x in radians. The input must be between -1 and 1.

**Example:** `ARCSIN(0.5)` ≈ 0.524 radians

#### `ARCCOS(x)`
Returns the arccosine of x in radians. The input must be between -1 and 1.

**Example:** `ARCCOS(0.5)` ≈ 1.047 radians

#### `ARCTAN(x)`
Returns the arctangent of x in radians.

**Example:** `ARCTAN(1)` ≈ 0.785 radians

### Exponential and Logarithmic Functions

#### `EXP(x)`
Returns e raised to the power of x (e^x).

**Example:** `EXP(1)` ≈ 2.718

#### `LN(x)`
Returns the natural logarithm of x (base e). The input must be positive.

**Example:** `LN(2.718)` ≈ 1

#### `LOG10(x)`
Returns the base-10 logarithm of x. The input must be positive.

**Example:** `LOG10(100)` = 2

#### `SQRT(x)`
Returns the square root of x. The input must be non-negative.

**Example:** `SQRT(16)` = 4

### Other Mathematical Functions

#### `ABS(x)`
Returns the absolute value of x.

**Example:** `ABS(-5)` = 5

#### `INT(x)`
Returns the largest integer less than or equal to x (floor function).

**Example:** `INT(3.7)` = 3, `INT(-2.3)` = -3

#### `SIGN(x)`
Returns the sign of x: 1 if x > 0, -1 if x < 0, and 0 if x = 0.

**Example:** `SIGN(-5)` = -1, `SIGN(0)` = 0, `SIGN(3)` = 1

#### `MAX(a, b)`
Returns the maximum of two values.

**Example:** `MAX(5, 10)` = 10

#### `MIN(a, b)`
Returns the minimum of two values.

**Example:** `MIN(5, 10)` = 5

#### `MEAN(x1, x2, ..., xn)`
Returns the arithmetic mean (average) of the arguments.

**Example:** `MEAN(2, 4, 6)` = 4

#### `SAFEDIV(numerator, denominator, default)`
Performs safe division. Returns `numerator / denominator` if denominator is not zero, otherwise returns `default`.

**Example:** `SAFEDIV(10, 2, 0)` = 5, `SAFEDIV(10, 0, 99)` = 99

### Constants

#### `PI`
The mathematical constant π (pi) ≈ 3.14159.

**Example:** `2 * PI` ≈ 6.283

#### `INF`
Represents positive infinity.

**Example:** `1 / INF` = 0

## Time-Based Functions

### Time Constants

#### `TIME`
Returns the current simulation time.

**Example:** At t=5.0, `TIME` = 5.0

#### `TIME_STEP` (or `DT`)
Returns the simulation time step (dt).

**Example:** If dt=0.25, `TIME_STEP` = 0.25

#### `INITIAL_TIME` (or `START_TIME`)
Returns the initial time of the simulation.

**Example:** If the simulation starts at t=0, `INITIAL_TIME` = 0

#### `FINAL_TIME`
Returns the final time of the simulation.

**Example:** If the simulation ends at t=100, `FINAL_TIME` = 100

### Test Input Functions

#### `STEP(height, step_time)`
Generates a step function that transitions from 0 to `height` at `step_time`.

**Parameters:**
- `height`: The height of the step
- `step_time`: The time at which the step occurs

**Example:** `STEP(10, 5)` returns 0 for t < 5 and 10 for t ≥ 5

#### `PULSE(volume, first_pulse, interval)`
Generates a pulse or series of pulses. The `volume` is distributed over the time step dt.

**Parameters:**
- `volume`: The total volume to be delivered in each pulse
- `first_pulse`: The time of the first pulse
- `interval` (optional): The time between pulses (0 for a single pulse)

**Example:** `PULSE(1, 5, 0)` delivers a pulse of volume 1 at time 5

#### `RAMP(slope, start_time, end_time)`
Generates a ramp function that increases linearly.

**Parameters:**
- `slope`: The rate of increase per time unit
- `start_time`: The time at which the ramp begins
- `end_time` (optional): The time at which the ramp ends

**Example:** `RAMP(2, 5, 10)` returns 0 for t ≤ 5, increases by 2 per time unit from t=5 to t=10, then remains constant

## Array Functions

Array functions operate on arrayed variables (variables with subscripts/dimensions).

#### `SIZE(array)`
Returns the size (number of elements) of an array dimension.

**Example:** For an array with subscript [Region] with 3 regions, `SIZE(population[Region])` = 3

#### `SUM(array)`
Returns the sum of all elements in an array.

**Example:** `SUM(sales[Region])` returns the total sales across all regions

#### `MEAN(array)`
Returns the mean (average) of all elements in an array.

**Example:** `MEAN(temperatures[Location])` returns the average temperature

#### `STDDEV(array)`
Returns the standard deviation of all elements in an array.

**Example:** `STDDEV(measurements[Sample])` returns the standard deviation of measurements

#### `RANK(array, dimension, order)`
Returns the rank (position) of elements in an array.

**Note:** Full implementation pending.

## Standard Library Functions

Simlin includes several standard library functions implemented as sub-models. These functions maintain internal state across timesteps.

### Smoothing Functions

#### `SMTH1(input, delay_time, initial_value)`
First-order exponential smoothing (single exponential smooth).

**Parameters:**
- `input`: The value to be smoothed
- `delay_time`: The time constant for smoothing (higher values = more smoothing)
- `initial_value`: The initial value of the smoothed variable

**Example:** `SMTH1(actual_sales, 3, 100)` smooths sales data with a 3-time-unit delay

#### `SMTH3(input, delay_time, initial_value)`
Third-order exponential smoothing. Provides smoother output than SMTH1 but with more lag.

**Parameters:**
- `input`: The value to be smoothed
- `delay_time`: The time constant for smoothing
- `initial_value`: The initial value of the smoothed variable

**Example:** `SMTH3(noisy_signal, 5, 50)` applies third-order smoothing

### Delay Functions

#### `DELAY1(input, delay_time, initial_value)`
First-order exponential delay. Delays the input signal by approximately `delay_time`.

**Parameters:**
- `input`: The value to be delayed
- `delay_time`: The delay time
- `initial_value`: The initial value in the delay

**Example:** `DELAY1(orders, 2, 100)` delays orders by approximately 2 time units

#### `DELAY3(input, delay_time, initial_value)`
Third-order exponential delay. Provides a more pipeline-like delay than DELAY1.

**Parameters:**
- `input`: The value to be delayed
- `delay_time`: The delay time
- `initial_value`: The initial value in the delay

**Example:** `DELAY3(shipments, 4, 50)` delays shipments by approximately 4 time units

### Trend Functions

#### `TREND(input, delay_time, initial_value)`
Calculates the trend (rate of change) of the input over time.

**Parameters:**
- `input`: The value whose trend is being calculated
- `delay_time`: The time period over which to calculate the trend
- `initial_value`: The initial value

**Example:** `TREND(population, 10, 1000)` calculates the population growth trend

### Special Functions

#### `PREVIOUS(input, initial_value)`
Returns the value of `input` from the previous time step.

**Parameters:**
- `input`: The variable whose previous value is needed
- `initial_value`: The value to return at the first time step

**Example:** `PREVIOUS(stock_level, 100)` returns the stock level from the previous timestep

#### `INIT(input)`
Returns the initial value of `input` (the value at the start of the simulation).

**Parameters:**
- `input`: The variable whose initial value is needed

**Example:** `INIT(population)` returns the initial population value

## Lookup Functions

#### `LOOKUP(table_name, input)`
Performs linear interpolation on a graphical function (lookup table).

**Parameters:**
- `table_name`: The name of the lookup table defined in the model
- `input`: The x-value to look up

**Example:** `LOOKUP(demand_curve, price)` returns the interpolated demand value for a given price

## Usage Notes

1. **Case Insensitivity**: Function names are case-insensitive in Simlin. `SIN`, `sin`, and `Sin` are all equivalent.

2. **Unit Checking**: Simlin performs unit checking on many builtin functions. Trigonometric functions expect dimensionless (radian) inputs, and operations like addition require compatible units.

3. **Array Support**: When array builtins like `SUM`, `MEAN`, `STDDEV`, and `SIZE` are used, they operate on the entire array or specified dimensions.

4. **Standard Library Implementation**: Functions like `SMTH1`, `DELAY1`, `TREND`, and `PREVIOUS` are implemented as complete sub-models in the `stdlib/` directory. They use stocks and flows to maintain state.

5. **Module Inputs**: The special function `ISMODULEINPUT()` is used internally for module definitions to test whether an input was provided.

## See Also

- [First Model Tutorial](./first-model.md) - Learn how to build your first model
- [Cheat Sheet](./cheat-sheet.md) - Quick reference for modeling
- [XMILE Specification](http://docs.oasis-open.org/xmile/xmile/v1.0/xmile-v1.0.html) - Standard format for system dynamics models
