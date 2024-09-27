[Previous](ACOS.md) [Next](ANY_VALUE.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. ADD_MONTHS 

## ADD_MONTHS

Syntax

![Description of add_months.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/add_months.gif)  
[Description of the illustration add_months.eps](img_text/add_months.md)

Purpose

`ADD_MONTHS` returns the date `date` plus `integer` months. A month is defined
by the session parameter `NLS_CALENDAR`. The date argument can be a datetime
value or any value that can be implicitly converted to `DATE`. The `integer`
argument can be an integer or any value that can be implicitly converted to an
integer. The return type is always `DATE`, regardless of the data type of
`date`. If `date` is the last day of the month or if the resulting month has
fewer days than the day component of `date`, then the result is the last day
of the resulting month. Otherwise, the result has the same day component as
`date`.

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion

Examples

The following example returns the month after the `hire_date` in the sample
table `employees`:

    
    
    SELECT TO_CHAR(ADD_MONTHS(hire_date, 1), 'DD-MON-YYYY') "Next month"
      FROM employees 
      WHERE last_name = 'Baer';
    
    Next Month
    -----------
    07-JUL-2002


[← Previous](ACOS.md)

[Next →](ANY_VALUE.md)
