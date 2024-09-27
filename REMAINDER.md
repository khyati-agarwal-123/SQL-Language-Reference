[Previous](REGR_-Linear-Regression-Functions.md) [Next](REPLACE.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. REMAINDER 

## REMAINDER

Syntax

![Description of remainder.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/remainder.gif)  
[Description of the illustration remainder.eps](img_text/remainder.md)

Purpose

`REMAINDER` returns the remainder of `n2` divided by `n1`.

This function takes as arguments any numeric data type or any nonnumeric data
type that can be implicitly converted to a numeric data type. Oracle
determines the argument with the highest numeric precedence, implicitly
converts the remaining arguments to that data type, and returns that data
type.

The `MOD` function is similar to `REMAINDER` except that it uses `FLOOR` in
its formula, whereas `REMAINDER` uses `ROUND`. Refer to
[MOD](MOD.md#GUID-E12A3928-2C50-45B0-B8C3-82432C751B8C).

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion and "[Numeric Precedence](Data-
Types.md#GUID-4C0B65DB-E751-4957-A1ED-5044BAFA7812)" for information on
numeric precedence

  * If `n1` = 0 or `n2` = infinity, then Oracle returns 

    * An error if the arguments are of type `NUMBER`

    * `NaN` if the arguments are `BINARY_FLOAT` or `BINARY_DOUBLE`. 

  * If `n1` != 0, then the remainder is `n2` \- (`n1`*`N`) where `N` is the integer nearest `n2`/`n1`. If `n2`/`n1` equals `x.5`, then `N` is the nearest even integer. 

  * If `n2` is a floating-point number, and if the remainder is 0, then the sign of the remainder is the sign of `n2`. Remainders of 0 are unsigned for `NUMBER` values. 

Examples

Using table `float_point_demo`, created for the `TO_BINARY_DOUBLE`
"[Examples](TO_BINARY_DOUBLE.md#GUID-0BA2E065-8006-426C-A3CB-1F6B0C8F283C__I1336203)",
the following example divides two floating-point numbers and returns the
remainder of that operation:

    
    
    SELECT bin_float, bin_double, REMAINDER(bin_float, bin_double)
      FROM float_point_demo;
    
     BIN_FLOAT BIN_DOUBLE REMAINDER(BIN_FLOAT,BIN_DOUBLE)
    ---------- ---------- -------------------------------
    1.235E+003 1.235E+003                      5.859E-005


[← Previous](REGR_-Linear-Regression-Functions.md)

[Next →](REPLACE.md)
