[Previous](JSON_OBJECT.md) [Next](JSON_QUERY.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. JSON_OBJECTAGG

## JSON_OBJECTAGG

Syntax

![Description of json_objectagg.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_objectagg.gif)  
[Description of the illustration
json_objectagg.eps](img_text/json_objectagg.md)

JSON_on_null_clause::=

![Description of json_on_null_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_on_null_clause.gif)  
[Description of the illustration
json_on_null_clause.eps](img_text/json_on_null_clause.md)

JSON_returning_clause::=

  

![Description of json_returning_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_returning_clause.gif)  
[Description of the illustration
json_returning_clause.eps](img_text/json_returning_clause.md)

  

Purpose

The SQL/JSON function `JSON_OBJECTAGG` is an aggregate function. It takes as
its input a property key-value pair. Typically, the property key, the property
value, or both are columns of SQL expressions. This function constructs an
object member for each key-value pair and returns a single JSON object that
contains those object members.

[KEY] string VALUE expr

Use this clause to specify property key-value pairs.

  * `KEY` is optional and is provided for semantic clarity. 

  * Use `string` to specify the property key name as a case-sensitive text literal. 

  * Use `expr` to specify the property value. For `expr`, you can specify any expression that evaluates to a SQL numeric literal, text literal, date, or timestamp. The date and timestamp data types are printed in the generated JSON object or array as JSON Strings following the ISO 8601 date format. If `expr` evaluates to a numeric literal, then the resulting property value is a JSON number value; otherwise, the resulting property value is a case-sensitive JSON string value enclosed in double quotation marks. 

FORMAT JSON

Use this optional clause to indicate that the input string is JSON, and will
therefore not be quoted in the output.

JSON_on_null_clause

Use this clause to specify the behavior of this function when `expr` evaluates
to null.

  * `NULL` `ON` `NULL` \- When NULL ON NULL is specified, then a JSON NULL value is used as a value for the given key. 

  * `ABSENT` `ON` `NULL` \- If you specify this clause, then the function omits the property key-value pair from the JSON object. 

JSON_returning_clause

Use this clause to specify the data type of the character string returned by
this function. You can specify the following data types:

  * `VARCHAR2[(``size` `[BYTE,CHAR])]`

When specifying the `VARCHAR2` data type elsewhere in SQL, you are required to
specify a size. However, in this clause you can omit the size.

  * `CLOB` to return a character large object containing single-byte or multi-byte characters. 

  * `BLOB` to return a binary large object of the `AL32UTF8` character set. 

  * `JSON` to return JSON data. 

You must set the database initialization parameter compatible to `20` or
greater to use the `JSON` data type.

If you omit this clause, or if you specify `VARCHAR2` but omit the `size`
value, then `JSON_OBJECTAGG` returns a character string of type
`VARCHAR2(4000)`.

Refer to "[Data Types](Data-
Types.md#GUID-A3C0D836-BADB-44E5-A5D4-265BA5968483)" for more information on
the preceding data types.

STRICT

Specify the `STRICT` clause to verify that the output of the JSON generation
function is correct JSON. If the check fails, a syntax error is raised.

Refer to
[JSON_OBJECT](JSON_OBJECT.md#GUID-1EF347AE-7FDA-4B41-AFE0-DD5A49E8B370) for
examples.

WITH UNIQUE KEYS

Specify `WITH UNIQUE KEYS` to guarantee that generated JSON objects have
unique keys.

Examples

The following example constructs a JSON object whose members contain
department names and department numbers:

    
    
    SELECT JSON_OBJECTAGG(KEY department_name VALUE department_id) "Department Numbers"
      FROM departments
      WHERE department_id <= 30;
    
    Department Numbers
    ----------------------------------------------------
    {"Administration":10,"Marketing":20,"Purchasing":30}


[← Previous](JSON_OBJECT.md)

[Next →](JSON_QUERY.md)
