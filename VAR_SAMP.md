[Previous](VAR_POP.md) [Next](VARIANCE.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. VAR_SAMP 

## VAR_SAMP

Syntax

![Description of var_samp.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/var_samp.gif)  
[Description of the illustration var_samp.eps](img_text/var_samp.md)

See Also:

"[Analytic Functions](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056)" for information on
syntax, semantics, and restrictions

Purpose

`VAR_SAMP` returns the sample variance of a set of numbers after discarding
the nulls in this set. You can use it as both an aggregate and analytic
function.

This function takes as an argument any numeric data type or any nonnumeric
data type that can be implicitly converted to a numeric data type. The
function returns the same data type as the numeric data type of the argument.

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion

If the function is applied to an empty set, then it returns null. The function
makes the following calculation:

    
    
    (SUM(expr - (SUM(expr) / COUNT(expr)))2) / (COUNT(expr) - 1)
    

This function is similar to `VARIANCE`, except that given an input set of one
element, `VARIANCE` returns 0 and `VAR_SAMP` returns null.

See Also:

"[About SQL Expressions](About-SQL-
Expressions.md#GUID-68789A5C-B142-496F-ADEE-837F75F95B2B)" for information
on valid forms of `expr` and "[Aggregate Functions](Aggregate-
Functions.md#GUID-62BE676B-AF18-4E63-BD14-25206FEA0848)"

Aggregate Example

The following example returns the sample variance of the salaries in the
sample `employees` table.

    
    
    SELECT VAR_SAMP(salary) FROM employees;
    
    VAR_SAMP(SALARY)
    ----------------
          15284813.7

Analytic Example

Refer to the analytic example for
[VAR_POP](VAR_POP.md#GUID-B62FB4A4-BD1F-47B0-B412-31A98B70C2E4).


[← Previous](VAR_POP.md)

[Next →](VARIANCE.md)
