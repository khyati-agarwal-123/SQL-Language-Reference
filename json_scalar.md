[Previous](JSON_QUERY.md) [Next](JSON_SERIALIZE.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. JSON_SCALAR

## JSON_SCALAR

Syntax

  

![Description of json_scalar.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_scalar.gif)  
[Description of the illustration json_scalar.eps](img_text/json_scalar.md)

  

Purpose

`JSON_SCALAR` accepts a SQL scalar value as input and returns a corresponding
JSON scalar value as a `JSON` type instance. In particular, the value can be
of an Oracle-specific JSON-language type, such as a date, which is not part of
the JSON standard.

The argument to `JSON_SCALAR` can be an instance of any of these SQL data
types: `BINARY_DOUBLE`, `BINARY_FLOAT`, `BLOB`, `CLOB`, `DATE`, `INTERVAL YEAR
TO MONTH`, `INTERVAL DAY TO SECOND`, `JSON`, `NUMBER`, `RAW`, `TIMESTAMP`,
`VARCHAR`, `VARCHAR2`, or `VECTOR`.

The returned `JSON` type instance is a JSON-language scalar value supported by
Oracle.

You can use the `JSON_SCALAR` function, only if the database initialization
parameter `compatible` is at least `20`. Otherwise it raises an error.

See Also:

See [Oracle SQL Function
JSON_SCALAR](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADJSN-GUID-5EAC1ADD-E138-4488-9FB0-7C245F87CBFD) of the
JSON Developer's Guide.


[← Previous](JSON_QUERY.md)

[Next →](JSON_SERIALIZE.md)
