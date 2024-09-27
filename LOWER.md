[Previous](LOG.md) [Next](LPAD.md) JavaScript must be enabled to correctly
display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. LOWER 

## LOWER

Syntax

![Description of lower.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lower.gif)  
[Description of the illustration lower.eps](img_text/lower.md)

Purpose

`LOWER` returns `char`, with all letters lowercase. `char` can be any of the
data types `CHAR`, `VARCHAR2`, `NCHAR`, `NVARCHAR2`, `CLOB`, or `NCLOB`. The
return value is the same data type as `char`. The database sets the case of
the characters based on the binary mapping defined for the underlying
character set. For linguistic-sensitive lowercase, refer to
[NLS_LOWER](NLS_LOWER.md#GUID-96944213-377E-461C-9F02-2DC4EC2B1649).

See Also:

Appendix C in [Oracle Database Globalization Support
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the
collation derivation rules, which define the collation assigned to the
character return value of `LOWER`

Examples

The following example returns a string in lowercase:

    
    
    SELECT LOWER('MR. SCOTT MCMILLAN') "Lowercase"
      FROM DUAL;
    
    Lowercase
    --------------------
    mr. scott mcmillan 


[← Previous](LOG.md)

[Next →](LPAD.md)
