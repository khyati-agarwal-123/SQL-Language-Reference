[Previous](STDDEV.md) [Next](STDDEV_SAMP.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. STDDEV_POP 

## STDDEV_POP

Syntax

![Description of stddev_pop.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/stddev_pop.gif)  
[Description of the illustration stddev_pop.eps](img_text/stddev_pop.md)

See Also:

"[Analytic Functions](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056)" for information on
syntax, semantics, and restrictions

Purpose

`STDDEV_POP` computes the population standard deviation and returns the square
root of the population variance. You can use it as both an aggregate and
analytic function.

This function takes as an argument any numeric data type or any nonnumeric
data type that can be implicitly converted to a numeric data type. The
function returns the same data type as the numeric data type of the argument.

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion

This function is the same as the square root of the `VAR_POP` function. When
`VAR_POP` returns null, this function returns null.

See Also:

  * "[Aggregate Functions](Aggregate-Functions.md#GUID-62BE676B-AF18-4E63-BD14-25206FEA0848)" and [VAR_POP](VAR_POP.md#GUID-B62FB4A4-BD1F-47B0-B412-31A98B70C2E4)

  * "[About SQL Expressions](About-SQL-Expressions.md#GUID-68789A5C-B142-496F-ADEE-837F75F95B2B)" for information on valid forms of `expr`

Aggregate Example

The following example returns the population and sample standard deviations of
the amount of sales in the sample table `sh.sales`:

    
    
    SELECT STDDEV_POP(amount_sold) "Pop", 
       STDDEV_SAMP(amount_sold) "Samp"
       FROM sales;
    
           Pop       Samp
    ---------- ----------
    896.355151 896.355592

Analytic Example

The following example returns the population standard deviations of salaries
in the sample `hr.employees` table by department:

    
    
    SELECT department_id, last_name, salary, 
       STDDEV_POP(salary) OVER (PARTITION BY department_id) AS pop_std
       FROM employees
       ORDER BY department_id, last_name, salary, pop_std;
    
    DEPARTMENT_ID LAST_NAME                     SALARY    POP_STD
    ------------- ------------------------- ---------- ----------
               10 Whalen                          4400          0
               20 Fay                             6000       3500
               20 Hartstein                      13000       3500
               30 Baida                           2900  3069.6091
    . . .
             100 Urman                           7800 1644.18166
              110 Gietz                           8300       1850
              110 Higgins                        12000       1850
                  Grant                           7000          0


[← Previous](STDDEV.md)

[Next →](STDDEV_SAMP.md)
