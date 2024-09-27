[Previous](COUNT.md) [Next](COVAR_SAMP.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. COVAR_POP 

## COVAR_POP

Syntax

![Description of covar_pop.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/covar_pop.gif)  
[Description of the illustration covar_pop.eps](img_text/covar_pop.md)

See Also:

"[Analytic Functions](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056)" for information on
syntax, semantics, and restrictions

Purpose

`COVAR_POP` returns the population covariance of a set of number pairs. You
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

Oracle Database applies the function to the set of (`expr1`, `expr2`) pairs
after eliminating all pairs for which either `expr1` or `expr2` is null. Then
Oracle makes the following computation:

    
    
    (SUM(expr1 * expr2) - SUM(expr2) * SUM(expr1) / n) / n
    

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

The following example calculates the population covariance and sample
covariance for time employed (`SYSDATE` \- `hire_date`) and salary using the
sample table `hr.employees`:

    
    
    SELECT job_id, 
           COVAR_POP(SYSDATE-hire_date, salary) AS covar_pop,
           COVAR_SAMP(SYSDATE-hire_date, salary) AS covar_samp
      FROM employees
      WHERE department_id in (50, 80)
      GROUP BY job_id
      ORDER BY job_id, covar_pop, covar_samp;
    
    JOB_ID       COVAR_POP  COVAR_SAMP
    ---------- ----------- -----------
    SA_MAN          660700      825875
    SA_REP      579988.466   600702.34
    SH_CLERK      212432.5  223613.158
    ST_CLERK     176577.25  185870.789
    ST_MAN          436092      545115

Analytic Example

The following example calculates cumulative sample covariance of the list
price and minimum price of the products in the sample schema `oe`:

    
    
    SELECT product_id, supplier_id,
           COVAR_POP(list_price, min_price) 
             OVER (ORDER BY product_id, supplier_id)
             AS CUM_COVP,
           COVAR_SAMP(list_price, min_price)
             OVER (ORDER BY product_id, supplier_id)
             AS CUM_COVS 
      FROM product_information p
      WHERE category_id = 29
      ORDER BY product_id, supplier_id;
    
    PRODUCT_ID SUPPLIER_ID   CUM_COVP   CUM_COVS
    ---------- ----------- ---------- ----------
          1774      103088          0
          1775      103087    1473.25     2946.5
          1794      103096 1702.77778 2554.16667
          1825      103093    1926.25 2568.33333
          2004      103086     1591.4    1989.25
          2005      103086     1512.5       1815
          2416      103088 1475.97959 1721.97619
    . . .


[← Previous](COUNT.md)

[Next →](COVAR_SAMP.md)
