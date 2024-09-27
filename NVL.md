[Previous](NUMTOYMINTERVAL.md) [Next](NVL2.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. NVL 

## NVL

Syntax

![Description of nvl.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/nvl.gif)  
[Description of the illustration nvl.eps](img_text/nvl.md)

Purpose

`NVL` lets you replace null (returned as a blank) with a string in the results
of a query. If `expr1` is null, then `NVL` returns `expr2`. If `expr1` is not
null, then `NVL` returns `expr1`.

The arguments `expr1` and `expr2` can have any data type. If their data types
are different, then Oracle Database implicitly converts one to the other. If
they cannot be converted implicitly, then the database returns an error. The
implicit conversion is implemented as follows:

  * If `expr1` is character data, then Oracle Database converts `expr2` to the data type of `expr1` before comparing them and returns `VARCHAR2` in the character set of `expr1`. 

  * If `expr1` is numeric, then Oracle Database determines which argument has the highest numeric precedence, implicitly converts the other argument to that data type, and returns that data type. 

See Also:

  * [Table 2-9](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell indicates implicit conversion of the data types") for more information on implicit conversion and "[Numeric Precedence](Data-Types.md#GUID-4C0B65DB-E751-4957-A1ED-5044BAFA7812)" for information on numeric precedence 

  * "[COALESCE](COALESCE.md#GUID-3F9007A7-C0CA-4707-9CBA-1DBF2CDE0C87)" and "[CASE Expressions](CASE-Expressions.md#GUID-CA29B333-572B-4E1D-BA64-851FABDBAE96)", which provide functionality similar to that of `NVL`

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the return value of `NVL` when it is a character value 

Examples

The following example returns a list of employee names and commissions,
substituting "Not Applicable" if the employee receives no commission:

    
    
    SELECT last_name, NVL(TO_CHAR(commission_pct), 'Not Applicable') commission
      FROM employees
      WHERE last_name LIKE 'B%'
      ORDER BY last_name;
     
    LAST_NAME                 COMMISSION
    ------------------------- ----------------------------------------
    Baer                      Not Applicable
    Baida                     Not Applicable
    Banda                     .1
    Bates                     .15
    Bell                      Not Applicable
    Bernstein                 .25
    Bissot                    Not Applicable
    Bloom                     .2
    Bull                      Not Applicable


[← Previous](NUMTOYMINTERVAL.md)

[Next →](NVL2.md)
