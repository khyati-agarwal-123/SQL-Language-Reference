[Previous](UNISTR.md) [Next](USER.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. UPPER 

## UPPER

Syntax

![Description of upper.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/upper.gif)  
[Description of the illustration upper.eps](img_text/upper.md)

Purpose

`UPPER` returns `char`, with all letters uppercase. `char` can be any of the
data types `CHAR`, `VARCHAR2`, `NCHAR`, `NVARCHAR2`, `CLOB`, or `NCLOB`. The
return value is the same data type as `char`. The database sets the case of
the characters based on the binary mapping defined for the underlying
character set. For linguistic-sensitive uppercase, refer to
[NLS_UPPER](NLS_UPPER.md#GUID-91D6302F-4DE2-49FA-8837-D46D3FD58DF8).

See Also:

Appendix C in [Oracle Database Globalization Support
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the
collation derivation rules, which define the collation assigned to the
character return value of `UPPER`

Examples

The following example returns each employee's last name in uppercase:

    
    
    SELECT UPPER(last_name) "Uppercase"
       FROM employees;


[← Previous](UNISTR.md)

[Next →](USER.md)
