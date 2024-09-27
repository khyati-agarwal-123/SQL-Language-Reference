[Previous](json-type-constructor.md) [Next](KURTOSIS_SAMP.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. KURTOSIS_POP

## KURTOSIS_POP

Syntax

![Description of kurtosis_pop.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/kurtosis_pop.gif)  
[Description of the illustration kurtosis_pop.eps](img_text/kurtosis_pop.md)

Purpose

The population kurtosis function `KURTOSIS_POP` is primarily used to determine
the characteristics of outliers in a given distribution.

NULL values in `expr` are ignored.

Returns NULL if all rows in the group have NULL `expr` values.

Returns 0 if there are one or two rows in `expr`.

For a given set of values, the result of population kurtosis (`KURTOSIS_POP`)
and sample kurtosis (`KURTOSIS_SAMP`) are always deterministic. However, the
values of `KURTOSIS_POP` and `KURTOSIS_SAMP` differ. As the number of values
in the data set increases, the difference between the computed values of
`KURTOSIS_SAMP` and `KURTOSIS_POP` decreases.


[← Previous](json-type-constructor.md)

[Next →](KURTOSIS_SAMP.md)
