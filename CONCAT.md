[Previous](CON_UID_TO_ID.md) [Next](CONVERT.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. CONCAT 

## CONCAT

Syntax

![Description of concat.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/concat.gif)  
[Description of the illustration concat.eps](img_text/concat.md)

Purpose

`CONCAT` takes as input two or more arguments and returns the concatenation of
all arguments.

The arguments can be any of the data types `CHAR`, `VARCHAR2`, `NCHAR`,
`NVARCHAR2`, `CLOB`, or `NCLOB`. Arguments of other data types are implicitly
converted to `VARCHAR2` before concatenation.

The string returned is in the same character set as `char1`. Its data type
depends on the data types of the arguments.

In concatenations of two or more different data types, Oracle Database returns
the data type that results in a lossless conversion. Therefore, if one of the
arguments is a LOB, then the returned value is a LOB. If one of the arguments
is a national data type, then the returned value is a national data type.

Rules for the Data Types of Return Values

Among all arguments:

  * if there is a NCLOB, or if there is a CLOB and a NVARCHAR2 /NCHAR, then the return type is NCLOB.

  * otherwise, if there is CLOB, then the return type is CLOB

  * otherwise, if there is NVARCHAR2, or if there is a VARCHAR2 and a NCHAR, then the return type is NVARCHAR2

  * otherwise, if there is VARCHAR2, then the return type is VARCHAR2

  * otherwise, if there is NCHAR, then the return type is NCHAR

  * otherwise, the return type is CHAR

Examples of Data Types Returned

`CONCAT`(`CLOB`, `NCLOB`) returns `NCLOB`

`CONCAT`(`CLOB`, `NCHAR`) returns `NCLOB`

`CONCAT`(`CLOB`, `CHAR`) returns `CLOB`

`CONCAT`(`VARCHAR2`, `NCHAR`) returns `NVARCHAR2`

`CONCAT`(`CHAR`, `VARCHAR2`) returns `VARCHAR2`

`CONCAT`(`CHAR`, `VARCHAR2`, `CLOB`) returns `CLOB`

`CONCAT`(`CHAR`, `NVARCHAR2`, `CLOB`) returns `NCLOB`

This function is equivalent to the concatenation operator (||).

See Also:

  * [Concatenation Operator](Concatenation-Operator.md#GUID-08C10738-706B-4290-B7CD-C279EBC90F7E) for information on the `CONCAT` operator 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of `CONCAT`

Examples

This example concatenates three character strings:

    
    
    SELECT CONCAT( last_name, '''s job category is ', job_id) "Job" 
      FROM employees 
      WHERE employee_id = 152;
     
    Job
    ------------------------------------------------------
    Hall's job category is SA_REP


[← Previous](CON_UID_TO_ID.md)

[Next →](CONVERT.md)
