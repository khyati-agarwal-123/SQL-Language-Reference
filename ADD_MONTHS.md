##  ADD_MONTHS {#GUID-B8C74443-DF32-4B7C-857F-28D557381543} 

Syntax 

![Description of add_months.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/add_months.gif)[ Description of the illustration add_months.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/add_months.md)

Purpose 

` ADD_MONTHS ` returns the date *date* plus *integer* months. A month is defined by the session parameter ` NLS_CALENDAR ` . The date argument can be a datetime value or any value that can be implicitly converted to ` DATE ` . The *integer* argument can be an integer or any value that can be implicitly converted to an integer. The return type is always ` DATE ` , regardless of the data type of *date* . If *date* is the last day of the month or if the resulting month has fewer days than the day component of *date* , then the result is the last day of the resulting month. Otherwise, the result has the same day component as *date* . 

> **note:** See Also: 

[ Table 2-9 ](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937) for more information on implicit conversion 

Examples 

The following example returns the month after the *hire_date* in the sample table ` employees ` : 
    
    
    ```
    SELECT TO_CHAR(ADD_MONTHS(hire_date, 1), 'DD-MON-YYYY') "Next month"
      FROM employees 
      WHERE last_name = 'Baer';
    
    Next Month
    -----------
    07-JUL-2002
    ```
