[Previous](CONVERT.md) [Next](CORR_A.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. CORR 

## CORR

Syntax

![Description of corr.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/corr.gif)  
[Description of the illustration corr.eps](img_text/corr.md)

See Also:

[Analytic Functions](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056) for information on
syntax, semantics, and restrictions

Purpose

`CORR` returns the coefficient of correlation of a set of number pairs. You
can use it as an aggregate or analytic function.

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

Oracle Database applies the function to the set of (`expr1`, `expr2`) after
eliminating the pairs for which either `expr1` or `expr2` is null. Then Oracle
makes the following computation:

    
    
    COVAR_POP(expr1, expr2) / (STDDEV_POP(expr1) * STDDEV_POP(expr2))
    

The function returns a value of type `NUMBER`. If the function is applied to
an empty set, then it returns null.

Note:

The `CORR` function calculates the Pearson's correlation coefficient, which
requires numeric expressions as arguments. Oracle also provides the `CORR_S`
(Spearman's rho coefficient) and `CORR_K` (Kendall's tau-b coefficient)
functions to support nonparametric or rank correlation.

See Also:

[Aggregate Functions](Aggregate-
Functions.md#GUID-62BE676B-AF18-4E63-BD14-25206FEA0848), [About SQL
Expressions](About-SQL-
Expressions.md#GUID-68789A5C-B142-496F-ADEE-837F75F95B2B) for information on
valid forms of `expr`, and
[CORR_*](CORR_A.md#GUID-B2DED35A-2ECE-4DF0-BDA4-28F28B7BCA23) for
information on the `CORR_S` and `CORR_K` functions

Aggregate Example

The following example calculates the coefficient of correlation between the
list prices and minimum prices of products by weight class in the sample table
`oe.product_information`:

    
    
    SELECT weight_class, CORR(list_price, min_price) "Correlation"
      FROM product_information
      GROUP BY weight_class
      ORDER BY weight_class, "Correlation";
    
    WEIGHT_CLASS Correlation
    ------------ -----------
               1  .999149795
               2  .999022941
               3  .998484472
               4  .999359909
               5  .999536087

Analytic Example

The following example shows the correlation between duration at the company
and salary by the employee's position. The result set shows the same
correlation for each employee in a given job:

    
    
    SELECT employee_id, job_id, 
           TO_CHAR((SYSDATE - hire_date) YEAR TO MONTH ) "Yrs-Mns",     salary, 
           CORR(SYSDATE-hire_date, salary)
           OVER(PARTITION BY job_id) AS "Correlation"
      FROM employees
      WHERE department_id in (50, 80)
      ORDER BY job_id, employee_id;
    
    EMPLOYEE_ID JOB_ID     Yrs-Mns     SALARY Correlation
    ----------- ---------- ------- ---------- -----------
            145 SA_MAN     +04-09       14000  .912385598
            146 SA_MAN     +04-06       13500  .912385598
            147 SA_MAN     +04-04       12000  .912385598
            148 SA_MAN     +01-08       11000  .912385598
            149 SA_MAN     +01-05       10500  .912385598
            150 SA_REP     +04-05       10000   .80436755
            151 SA_REP     +04-03        9500   .80436755
            152 SA_REP     +03-10        9000   .80436755
            153 SA_REP     +03-03        8000   .80436755
            154 SA_REP     +02-07        7500   .80436755
            155 SA_REP     +01-07        7000   .80436755
    . . .


[← Previous](CONVERT.md)

[Next →](CORR_A.md)
