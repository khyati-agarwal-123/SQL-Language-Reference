[Previous](ITERATION_NUMBER.md) [Next](JSON_ARRAYAGG.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. JSON_ARRAY

## JSON_ARRAY

Syntax

![Description of json_array.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_array.gif)  
[Description of the illustration json_array.eps](img_text/json_array.md)

JSON_ARRAY_content

  

![Description of json_array_content.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_array_content.gif)  
[Description of the illustration
json_array_content.eps](img_text/json_array_content.md)

  

JSON_ARRAY_enumeration_content::=

![Description of json_array_enumeration_content.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_array_enumeration_content.gif)  
[Description of the illustration
json_array_enumeration_content.eps](img_text/json_array_enumeration_content.md)

JSON_ARRAY_element

  

![Description of json_array_element.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_array_element.gif)  
[Description of the illustration
json_array_element.eps](img_text/json_array_element.md)

  

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

JSON_ARRAY_query_content::=

![Description of json_array_query_content.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_array_query_content.gif)  
[Description of the illustration
json_array_query_content.eps](img_text/json_array_query_content.md)

Purpose

The SQL/JSON function `JSON_ARRAY` takes as its input a sequence of SQL scalar
expressions or one collection type instance, `VARRAY` or `NESTED TABLE`.

It converts each expression to a JSON value, and returns a JSON array that
contains those JSON values.

If an ADT has a member which is a collection than the type mapping creates a
JSON object for the ADT with a nested JSON array for the collection member.

If a collection contains ADT instances then the type mapping will create a
JSON array of JSON objects.

Note:

[Generation of JSON Data Using
SQL](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADJSN-GUID-F942D202-E4BB-4ED8-997E-AEBD6D8ED8C1) of the
JSON Developer's Guide.

JSON_ARRAY_content

Use this clause to define the input to the `JSON_ARRAY` function.

JSON_ARRAY_element

  * expr

For `expr`, you can specify any SQL expression that evaluates to a JSON
object, a JSON array, a numeric literal, a text literal, date, timestamp, or
null. This function converts a numeric literal to a JSON number value, and a
text literal to a JSON string value. The date and timestamp data types are
printed in the generated JSON object or array as JSON Strings following the
ISO 8601 date format.

  * format_clause

You can specify `FORMAT JSON` to indicate that the input string is JSON, and
will therefore not be quoted in the output.

JSON_on_null_clause

Use this clause to specify the behavior of this function when `expr` evaluates
to null.

  * `NULL` `ON` `NULL` \- If you specify this clause, then the function returns the JSON null value. 

  * `ABSENT` `ON` `NULL` \- If you specify this clause, then the function omits the value from the JSON array. This is the default. 

JSON_returning_clause

Use this clause to specify the type of return value. One of :

  * `BLOB` to return a binary large object of the `AL32UTF8` character set. 

  * `CLOB` to return a character large object containing single-byte or multi-byte characters. 

  * `VARCHAR2` specifying the size as a number of bytes or characters. The default is bytes. If you omit this clause, or specify the clause without specifying the `size` value, then `JSON_ARRAY` returns a character string of type `VARCHAR2(4000)`. Refer to [VARCHAR2 Data Type](Data-Types.md#GUID-0DC7FFAA-F03F-4448-8487-F2592496A510) for more information. Note that when specifying the `VARCHAR2` data type elsewhere in SQL, you are required to specify a size. However, in the `JSON_returning_clause` you can omit the size. 

  * `BOOLEAN`

  * `JSON`

  * `VECTOR`

STRICT

Specify the `STRICT` clause to verify that the output of the JSON generation
function is correct JSON. If the check fails, a syntax error is raised.

Refer to
[JSON_OBJECT](JSON_OBJECT.md#GUID-1EF347AE-7FDA-4B41-AFE0-DD5A49E8B370) for
examples.

Examples

The following example constructs a JSON array from a JSON object, a JSON
array, a numeric literal, a text literal, and null:

    
    
    SELECT JSON_ARRAY (     
        JSON_OBJECT('percentage' VALUE .50),
        JSON_ARRAY(1,2,3),
        100,
        'California',
        null
        NULL ON NULL
        ) "JSON Array Example"
      FROM DUAL;
     
    JSON Array Example
    --------------------------------------------------------------------------------
    [{"percentage":0.5},[1,2,3],100,"California",null]


[← Previous](ITERATION_NUMBER.md)

[Next →](JSON_ARRAYAGG.md)
