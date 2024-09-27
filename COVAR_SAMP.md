[Previous](COVAR_POP.md) [Next](CUBE_TABLE.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. COVAR_SAMP 

## COVAR_SAMP

Syntax

![Description of covar_samp.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/covar_samp.gif)  
[Description of the illustration covar_samp.eps](img_text/covar_samp.md)

See Also:

[Analytic Functions](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056) for information on
syntax, semantics, and restrictions

Purpose

`COVAR_SAMP` returns the sample covariance of a set of number pairs. You can
use it as an aggregate or analytic function.

This function takes as arguments any numeric data type or any nonnumeric data
type that can be implicitly converted to a numeric data type. Oracle
determines the argument with the highest numeric precedence, implicitly
converts the remaining arguments to that data type, and returns that data
type.

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion and [Numeric Precedence](Data-
Types.md#GUID-4C0B65DB-E751-4957-A1ED-5044BAFA7812) for information on
numeric precedence

Oracle Database applies the function to the set of (`expr1`, `expr2`) pairs
after eliminating all pairs for which either `expr1` or `expr2` is null. Then
Oracle makes the following computation:

    
    
    (SUM(expr1 * expr2) - SUM(expr1) * SUM(expr2) / n) / (n-1)
    

where `n` is the number of (`expr1`, `expr2`) pairs where neither `expr1` nor
`expr2` is null.

The function returns a value of type `NUMBER`. If the function is applied to
an empty set, then it returns null.

See Also:

[About SQL Expressions](About-SQL-
Expressions.md#GUID-68789A5C-B142-496F-ADEE-837F75F95B2B) for information on
valid forms of `expr` and [Aggregate Functions](Aggregate-
Functions.md#GUID-62BE676B-AF18-4E63-BD14-25206FEA0848)

Aggregate Example

Refer to the aggregate example for
[COVAR_POP](COVAR_POP.md#GUID-D728D05F-D2E3-405C-986F-088B8353553A).

Analytic Example

Refer to the analytic example for
[COVAR_POP](COVAR_POP.md#GUID-D728D05F-D2E3-405C-986F-088B8353553A).


[← Previous](COVAR_POP.md)

[Next →](CUBE_TABLE.md)
