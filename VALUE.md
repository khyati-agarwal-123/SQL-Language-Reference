[Previous](VALIDATE_CONVERSION.md) [Next](VAR_POP.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. VALUE 

## VALUE

Syntax

![Description of value.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/value.gif)  
[Description of the illustration value.eps](img_text/value.md)

Purpose

`VALUE` takes as its argument a correlation variable (table alias) associated
with a row of an object table and returns object instances stored in the
object table. The type of the object instances is the same type as the object
table.

Examples

The following example uses the sample table `oe.persons`, which is created in
"[Substitutable Table and Column Examples](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2090577)":

    
    
    SELECT VALUE(p) FROM persons p;
    
    VALUE(P)(NAME, SSN)
    -------------------------------------------------------------
    PERSON_T('Bob', 1234)
    EMPLOYEE_T('Joe', 32456, 12, 100000)
    PART_TIME_EMP_T('Tim', 5678, 13, 1000, 20)

See Also:

"[IS OF type Condition](IS-OF-type-
Condition.md#GUID-7254E4C7-0194-4C1F-A3B2-2CFB0AD907CD)" for information on
using `IS` `OF` type conditions with the `VALUE` function


[← Previous](VALIDATE_CONVERSION.md)

[Next →](VAR_POP.md)
