[Previous](value-expressions-graph_table.md) [Next](Expressions.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Operators](Operators.md)
  3. JSON_ID Operator

## JSON_ID Operator

Syntax

  

![Description of json_id.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_id.gif)  
[Description of the illustration json_id.eps](img_text/json_id.md)

  

Purpose

`JSON_ID` takes a single argument, one of `'OID'` or `'UUID'` to create a
value for a document-identifier field that you provide.

`JSON_ID` returns a value of SQL type `RAW` that is globally unique. The value
returned is determined by the argument that you provide. With string `'OID'`,
a 12-byte `RAW` value is returned; with string `'UUID'`, a 16-byte `RAW` value
is returned.

See Also:

[JSON Collections](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADJSN-GUID-F69A381E-7A6A-4D18-A148-B0C541C174BD) of the
JSON Developer's Guide.


[← Previous](value-expressions-graph_table.md)

[Next →](Expressions.md)
