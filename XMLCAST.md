[Previous](XMLAGG.md) [Next](XMLCDATA.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. XMLCAST

## XMLCAST

Syntax

![Description of xmlcast.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/xmlcast.gif)  
[Description of the illustration xmlcast.eps](img_text/xmlcast.md)

Purpose

`XMLCast` casts `value_expression` to the scalar SQL data type specified by
`datatype`. The `value_expression` argument is a SQL expression that is
evaluated. The `datatype` argument can be of data type `NUMBER`, `VARCHAR2`,
`CHAR`, `CLOB`, `BLOB`, `REF` `XMLTYPE`, and any of the datetime data types.

See Also:

  * [Oracle XML DB Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADXDB0400) for more information on uses for this function and examples 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the return value of `XMLCAST` when it is a character value 


[← Previous](XMLAGG.md)

[Next →](XMLCDATA.md)
