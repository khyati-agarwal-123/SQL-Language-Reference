[Previous](XMLAGG.html) [Next](XMLCDATA.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)
  2. [Functions](Functions.html)
  3. XMLCAST



## XMLCAST

Syntax

![Description of xmlcast.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/xmlcast.gif)[Description of the illustration xmlcast.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/xmlcast.html)([datatype::=](Data-Types.html#GUID-A3C0D836-BADB-44E5-A5D4-265BA5968483__SECTION_KLC_CHG_DDC)) 

Purpose

`XMLCast` casts `value_expression` to the scalar SQL data type specified by `datatype`. The `value_expression` argument is a SQL expression that is evaluated. 

datatype

The `datatype` argument can be of data type `NUMBER`, `VARCHAR2`, `VARCHAR`, `CHAR`, `CLOB`, `BLOB`, `REF` `XMLTYPE`, and any of the datetime data types. 

`BLOB`, or `CLOB` with options `reference` or `value`. The default is `reference`. 

See Also:

  * [Oracle XML DB Developer's Guide](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADXDB0400) for more information on uses for this function and examples 

  * Appendix C in [Oracle Database Globalization Support Guide](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the return value of `XMLCAST` when it is a character value 




[← Previous](XMLAGG.md)

[Next →](XMLCDATA.md)
