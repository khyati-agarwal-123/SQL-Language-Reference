[Previous](JSON_DATAGUIDE.md) [Next](JSON_OBJECT.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. JSON_MERGEPATCH

## JSON_MERGEPATCH

Syntax

  

![Description of json_mergepatch.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_mergepatch.gif)  
[Description of the illustration
json_mergepatch.eps](img_text/json_mergepatch.md)

  

JSON_returning_clause::=

  

![Description of json_returning_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_returning_clause.gif)  
[Description of the illustration
json_returning_clause.eps](img_text/json_returning_clause.md)

  

json_on_error_clause::=

  

![Description of json_on_error_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_on_error_clause.gif)  
[Description of the illustration
json_on_error_clause.eps](img_text/json_on_error_clause.md)

  

Purpose

You can use the `JSON_MERGEPATCH` function to update specific portions of a
JSON document. You pass it a JSON Merge Patch document in `JSON_patch_expr`,
which specifies the changes to make to a specified JSON document, the
`JSON_target_expr`.

`JSON_MERGEPATCH` evaluates the patch document against the target document to
produce the result document. If the target or the patch document is NULL, then
the result is also NULL.

You can input any SQL datatype that supports JSON data: `JSON`, `VARCHAR2`,
`CLOB`, or `BLOB`. The function returns any of the SQL datatypes as output.

Data type `JSON` is available only if database initialization parameter
compatible is `20` or greater.

The default return type depends on the input data type. If the input type is
`JSON`, then `JSON` is also the default return type. Otherwise, `VARCHAR2` is
the default return type.

The `JSON_returning_clause` specifies the return type of the operator. The
default return type is `VARCHAR2(4000)`.

The `PRETTY` keyword specifies that the result should be formatted for human
readability.

The `ASCII` keyword specifies that non-ASCII characters should be output using
JSON escape sequences.

The `TRUNCATE` keyword specifies that the result document should be truncated
to fit in the specified return type.

The `JSON_on_error_clause` optionally controls the handling of errors that
occur during the processing of the target and patch documents.

  * `NULL ON ERROR` \- Returns null when an error occurs. This is the default. 
  * `ERROR ON ERROR` \- Returns the appropriate Oracle error when an error occurs. 

See Also:

  * [RFC 7396 JSON Merge Patch](https://tools.ietf.org/html/rfc7396)

  * [Updating a JSON Document with JSON Merge Patch](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADJSN-GUID-31F88F28-3D92-489B-9CCD-BD1931B91F1F)


[← Previous](JSON_DATAGUIDE.md)

[Next →](JSON_OBJECT.md)
