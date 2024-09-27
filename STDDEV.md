[Previous](STATS_WSR_TEST.md) [Next](STDDEV_POP.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. STDDEV 

## STDDEV

Syntax

![Description of stddev.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/stddev.gif)  
[Description of the illustration stddev.eps](img_text/stddev.md)

See Also:

"[Analytic Functions](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056)" for information on
syntax, semantics, and restrictions

Purpose

`STDDEV` returns the sample standard deviation of `expr`, a set of numbers.
You can use it as both an aggregate and analytic function. It differs from
`STDDEV_SAMP` in that `STDDEV` returns zero when it has only 1 row of input
data, whereas `STDDEV_SAMP` returns null.

Oracle Database calculates the standard deviation as the square root of the
variance defined for the `VARIANCE` aggregate function.

This function takes as an argument any numeric data type or any nonnumeric
data type that can be implicitly converted to a numeric data type. The
function returns the same data type as the numeric data type of the argument.

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion

If you specify `DISTINCT`, then you can specify only the
`query_partition_clause` of the `analytic_clause`. The `order_by_clause` and
`windowing_clause` are not allowed.

See Also:

  * "[Aggregate Functions](Aggregate-Functions.md#GUID-62BE676B-AF18-4E63-BD14-25206FEA0848)", [VARIANCE](VARIANCE.md#GUID-EC33717A-2509-402D-B3BB-7EECB2E4ED8B), and [STDDEV_SAMP](STDDEV_SAMP.md#GUID-7B2A708E-E73A-4CFE-978E-3F9C4BD37467)

  * "[About SQL Expressions](About-SQL-Expressions.md#GUID-68789A5C-B142-496F-ADEE-837F75F95B2B)" for information on valid forms of `expr`

Aggregate Examples

The following example returns the standard deviation of the salaries in the
sample `hr.employees` table:

    
    
    SELECT STDDEV(salary) "Deviation"
       FROM employees;
     
     Deviation
    ----------
    3909.36575

Analytic Examples

The query in the following example returns the cumulative standard deviation
of the salaries in Department 80 in the sample table `hr.employees`, ordered
by `hire_date`:

    
    
    SELECT last_name, salary, 
       STDDEV(salary) OVER (ORDER BY hire_date) "StdDev"
       FROM employees  
       WHERE department_id = 30
       ORDER BY last_name, salary, "StdDev"; 
     
    LAST_NAME                     SALARY     StdDev
    ------------------------- ---------- ----------
    Baida                           2900 4035.26125
    Colmenares                      2500 3362.58829
    Himuro                          2600  3649.2465
    Khoo                            3100 5586.14357
    Raphaely                       11000          0
    Tobias                          2800  4650.0896


[← Previous](STATS_WSR_TEST.md)

[Next →](STDDEV_POP.md)
