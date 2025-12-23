The XMILE standard behind Simlin includes a variety of builtin functions that can be used within equations for stocks, flows, and variables. These functions help perform mathematical calculations, manipulate strings, and handle arrays, among other tasks.

Here are some examples how builtin functions can be used in equations:

# Time Functions

## `TIME`

Returns the current simulation time.

This function can be used to change the output of an equation at specific times during the simulation.

For example, assume a model where a stock like a bath tub gets increased by a flow, i.e. water flows into the tub. You want the inflow to start with a rate of 0 per time unit. After 10 time units it should increase to 1. You can use the `TIME` function in an IF THEN ELSE statement to achieve this:

``` xmile
IF TIME >= 10 THEN 1 ELSE 0
```
