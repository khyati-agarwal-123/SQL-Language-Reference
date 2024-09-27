[Previous](CORR.md) [Next](COS.md) JavaScript must be enabled to correctly
display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. CORR_* 

## CORR_*

The `CORR_`* functions are:

  * `CORR_S`

  * `CORR_K`

Syntax

correlation::=

![Description of correlation.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/correlation.gif)  
[Description of the illustration correlation.eps](img_text/correlation.md)

Purpose

The `CORR` function (see
[CORR](CORR.md#GUID-E73AF5E2-38A4-436A-955C-5122C079F49C)) calculates the
Pearson's correlation coefficient and requires numeric expressions as input.
The `CORR_`* functions support nonparametric or rank correlation. They let you
find correlations between expressions that are ordinal scaled (where a ranking
of the values is possible). Correlation coefficients take on a value ranging
from -1 to 1, where 1 indicates a perfect relationship, -1 a perfect inverse
relationship (when one variable increases as the other decreases), and a value
close to 0 means no relationship.

These functions take two mandatory arguments, `expr1` and `expr2`, and an
optional third argument. The return value of the functions is a `NUMBER.`

The mandatory arguments are the two variables being analyzed. They can be of
any data type that is comparable other than `LONG`, `CLOB`, `BLOB`, `BFILE`,
or `VECTOR`. If the data type is a user-defined type (UDT), it must have a
`MAP` or `ORDER` method to be comparable.

The third argument specifies the variant of the result returned by the
functions. It is of type `VARCHAR2` and must be a constant expression, for
example, a character literal. If you omit the third argument, then the default
is` 'COEFFICIENT'`. The allowed argument values and their meaning are shown in
Table 7-2 [Table
7-2](CORR_A.md#GUID-B2DED35A-2ECE-4DF0-BDA4-28F28B7BCA23__GUID-
AB5A91D9-9BA9-4F91-90A7-E0C457FDB889 "The first column lists the values you
can specify for the return value of the function and the second column
explains how each value is interpreted."):

See Also:

  * [Table 2-9](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell indicates implicit conversion of the data types") for more information on implicit conversion and [Numeric Precedence](Data-Types.md#GUID-4C0B65DB-E751-4957-A1ED-5044BAFA7812) for information on numeric precedence 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation determination rules, which define the collation `CORR_K` and `CORR_S` use to compare characters from `expr1` with characters from `expr2`

Table 7-2 CORR_* Return Values

Return Value | Meaning  
---|---  
`'COEFFICIENT'` |  Coefficient of correlation  
`'ONE_SIDED_SIG'` |  Positive one-tailed significance of the correlation  
`'ONE_SIDED_SIG_POS'` |  Same as `ONE_SIDED_SIG`  
`'ONE_SIDED_SIG_NEG'` |  Negative one-tailed significance of the correlation  
`'TWO_SIDED_SIG'` |  Two-tailed significance of the correlation  
  
### CORR_S

`CORR_S` calculates the Spearman's rho correlation coefficient. The input
expressions should be a set of (xi, yi) pairs of observations. The function
first replaces each value with a rank. Each value of xi is replaced with its
rank among all the other xis in the sample, and each value of yi is replaced
with its rank among all the other yis. Thus, each xi and yi take on a value
from 1 to `n`, where `n` is the total number of pairs of values. Ties are
assigned the average of the ranks they would have had if their values had been
slightly different. Then the function calculates the linear correlation
coefficient of the ranks.

CORR_S Example

Using Spearman's rho correlation coefficient, the following example derives a
coefficient of correlation for each of two different comparisons -- `salary`
and `commission_pct`, and `salary` and `employee_id`:

    
    
    SELECT COUNT(*) count,
           CORR_S(salary, commission_pct) commission,
           CORR_S(salary, employee_id) empid
      FROM employees;
     
         COUNT COMMISSION      EMPID
    ---------- ---------- ----------
           107 .735837022 -.04473016

### CORR_K

`CORR_K` calculates the Kendall's tau-b correlation coefficient. As for
`CORR_S`, the input expressions are a set of (xi, yi) pairs of observations.
To calculate the coefficient, the function counts the number of concordant and
discordant pairs. A pair of observations is concordant if the observation with
the larger x also has a larger value of y. A pair of observations is
discordant if the observation with the larger x has a smaller y.

The significance of tau-b is the probability that the correlation indicated by
tau-b was due to chanceâa value of 0 to 1. A small value indicates a
significant correlation for positive values of tau-b (or anticorrelation for
negative values of tau-b).

CORR_K Example

Using Kendall's tau-b correlation coefficient, the following example
determines whether a correlation exists between an employee's salary and
commission percent:

    
    
    SELECT CORR_K(salary, commission_pct, 'COEFFICIENT') coefficient,
           CORR_K(salary, commission_pct, 'TWO_SIDED_SIG') two_sided_p_value
      FROM employees;
    
    COEFFICIENT TWO_SIDED_P_VALUE
    ----------- -----------------
     .603079768        3.4702E-07


[← Previous](CORR_A.md)

[Next →](COS.md)
