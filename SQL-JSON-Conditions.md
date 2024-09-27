[Previous](XML-Conditions.md) [Next](Compound-Conditions.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Conditions](Conditions.md)
  3. SQL For JSON Conditions

## SQL For JSON Conditions

SQL for JSON conditions allow you to test JavaScript Object Notation (JSON)
data as follows:

  * [IS JSON Condition](SQL-JSON-Conditions.md#GUID-99B9493D-2929-4A09-BA39-A56F8E7319DA) lets you test whether an expression is syntactically correct JSON data 

  * [JSON_EQUAL Condition](SQL-JSON-Conditions.md#GUID-35C7012D-FCDB-4106-88C1-CABA78326896) tests whether two JSON values are the same. 

  * [JSON_EXISTS Condition](SQL-JSON-Conditions.md#GUID-57762C80-0C8A-4B18-9BA7-9B3F5ABDC988) lets you test whether a specified JSON value exists in JSON data 

  * [JSON_TEXTCONTAINS Condition](SQL-JSON-Conditions.md#GUID-DEF7941B-1267-44E7-8514-5CD448503179) lets you test whether a specified character string exists in JSON property values. 

JSON_condition::=

![Description of json_condition.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_condition.gif)  
[Description of the illustration
json_condition.eps](img_text/json_condition.md)

### IS JSON Condition

Use this SQL JSON condition to test whether an expression is syntactically
correct, well-formed, JSON data.

  * If the data tested is syntactically correct and keyword `VALIDATE` is not present, then `IS JSON` returns true, and `IS NOT JSON` returns false. 

  * If keyword `VALIDATE` is present, then the data is tested to ensure that it is both well-formed and valid with respect to the specified JSON schema. Keyword `VALIDATE` (optionally followed by keyword `USING`) must be followed by a SQL string literal that is the JSON schema to validate against. 

  * If an error occurs during parsing or validating, and the data is considered to not be well-formed or not valid, then `IS JSON` returns false and `IS NOT JSON` returns true. Parsing and validation errors are handled by the condition itself returning true or false. Other errors that are neither from parsing or validation, these errors are raised. 

  * You can use `IS JSON` and `IS NOT JSON` in a `CASE` expression or the `WHERE` clause of a `SELECT` statement. You can use `IS JSON` in a check constraint. 

is_JSON_condition::=

![Description of is_json_condition.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/is_json_condition.gif)  
[Description of the illustration
is_json_condition.eps](img_text/is_json_condition.md)

is_json_args::=

  

![Description of is_json_args.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/is_json_args.gif)  
[Description of the illustration is_json_args.eps](img_text/is_json_args.md)

  

JSON_modifier_list::=

  

![Description of json_modifier_list.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_modifier_list.gif)  
[Description of the illustration
json_modifier_list.eps](img_text/json_modifier_list.md)

  

JSON_column_modifier::=

  

![Description of json_column_modifier.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_column_modifier.gif)  
[Description of the illustration
json_column_modifier.eps](img_text/json_column_modifier.md)

  

JSON_scalar_modifier::=

  

![Description of json_scalar_modifier.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_scalar_modifier.gif)  
[Description of the illustration
json_scalar_modifier.eps](img_text/json_scalar_modifier.md)

  

  * Use `expr` to specify the JSON data to be evaluated. Specify an expression that evaluates to a text literal. If `expr` is a column, then the column must be of data type `VARCHAR2`, `CLOB`, or `BLOB`. If `expr` evaluates to null or a text literal of length zero, then this condition returns `UNKNOWN`. 

  * You must specify `FORMAT` `JSON` if `expr` is a column of data type `BLOB`. 

  * If you specify `STRICT`, then this condition considers only strict JSON syntax to be well-formed JSON data. If you specify `LAX`, then this condition also considers lax JSON syntax to be well-formed JSON data. The default is `LAX`. Refer to [Oracle Database JSON Developerâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADJSN-GUID-1B6CFFBE-85FE-41DD-BA14-DD1DE73EAB20) for more information on strict and lax JSON syntax. 

  * If you specify `WITH` `UNIQUE` `KEYS`, then this condition considers JSON data to be well-formed only if key names are unique within each object. If you specify `WITHOUT` `UNIQUE` `KEYS`, then this condition considers JSON data to be well-formed even if duplicate key names occur within an object. A `WITHOUT` `UNIQUE` `KEYS` test performs faster than a `WITH` `UNIQUE` `KEYS` test. The default is `WITHOUT` `UNIQUE` `KEYS`. 

  * Specify the optional keyword `VALIDATE` to test that the data is also valid with respect to a given JSON schema. 

  * To enforce that a JSON type value is a certain type, you can use JSON type modifiers. See [SQL/JSON Conditions IS JSON and IS NOT JSON](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADJSN-GUID-8F897ED9-791B-4F53-AFAE-690DE38111D1) of the JSON Developer's Guide.

JSON Schema Validation

A JSON schema typically specifies the allowed structure and data typing of
other JSON documents. You can therefore use a JSON schema to validate JSON
data. You can validate JSON data against a JSON schema in the following ways:

  * Use condition `IS JSON` (or `IS NOT JSON`) with keyword `VALIDATE` and the name of a JSON schema, to test whether targeted data is valid (or invalid) against that schema. The schema can be provided as a literal string or a usage domain. (Keyword `VALIDATE` can optionally be followed by keyword `USING`.) 

You can use `VALIDATE` with condition is json anywhere you can use that
condition. This includes use in a `WHERE` clause, or as a check constraint to
ensure that only valid data is inserted in a column.

When used as a check constraint for a JSON-type column, you can alternatively
omit is json, and just use keyword `VALIDATE` directly. These two table
creations are equivalent, for a JSON-type column:

    
        CREATE TABLE tab (jcol JSON VALIDATE '{"type" : "object"}â);
    
        CREATE TABLE tab (jcol JSON CONSTRAINT jchk
      CHECK (jcol IS JSON VALIDATE '{"type" : "object"}â));

  * Use a usage domain as a check constraint for JSON type data. For example: 
    
        CREATE DOMAIN jd AS JSON CONSTRAINT jchkd CHECK (jd IS JSON VALIDATE '{"type" : "object"});
    
        CREATE TABLE jtab(jcol JSON DOMAIN jd);

When creating a domain from a schema, you can alternatively omit the
constraint and is json, and just use keyword `VALIDATE` directly. This domain
creation is equivalent to the previous one:

    
        CREATE DOMAIN jd AS JSON VALIDATE '{"type" : "object"};

  * For databases that support a binary JSON format, data can be encoded on the client. In such cases, the database does not have to convert textual JSON to its binary representation and hence validation using an extended data type can be performed.

If textual JSON is sent to the database, it is followed by an encoding process
to a binary representation (server-side encoding). In such circumstances, the
schema validator can operate in `CAST` mode. That is, the binary encoder can
use the value specified for the extended data type keyword in the JSON schema
and encode the scalar field to its binary representation. Only scaler types
are eligible for casting.

    
        CREATE TABLE jtab (
      id    NUMBER(9) PRIMARY KEY,
      jcol  JSON CHECK(jcol IS JSON VALIDATE CAST USING '{
                      "type": "object",
                      "properties": {
                           "firstName": {
                            "extendedType": "string",
                            "maxLength": 50
                          },
                          "birthDate" : {
                            "extendedType": "date"
                          }
                        },
                        "required": ["firstName", "birthDate"]
                      }'
      )
    );

The following textual JSON is a valid document per the above schema:

    
        {
      "firstName": "Scott",
      "birthDate": "1990-04-02"
    }

  * Use PL/SQL functions explained fully in [JSON Schema](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADJSN-GUID-7D67DF73-CB21-4878-AF93-D1A213411EC0) of the JSON Developer's Guide. 

Static dictionary views `DBA_JSON_SCHEMA_COLUMNS`, `ALL_JSON_SCHEMA_COLUMNS`,
and `USER_JSON_SCHEMA_COLUMNS` describe a JSON schema that you is used as a
check constraint.

Each row of these views contains the name of the table, the JSON column, and
the constraint defined by the JSON schema, as well as the JSON schema itself
and an indication of whether the cast mode is specified for the JSON schema.
Views `DBA_JSON_SCHEMA_COLUMNS` and `ALL_JSON_SCHEMA_COLUMNS` also contain the
name of the table owner.

Examples

IS JSON VALIDATE

The following exampe creates a schema `jsontab1` with a JSON constraint
`jtlisj` that has a JSON validate check:

    
    
    CREATE TABLE jsontab1(
        id NUMBER(4),
        j  JSON CONSTRAINT jt1isj CHECK (j IS JSON VALIDATE USING     
         '{
           "type":"object", 
           "minProperties": 2
          }')
        );

The following example shows the error when you try to insert values other than
a JSON object:

    
    
    INSERT INTO jsontab1(j) VALUES ('["a", "b"]');
    INSERT INTO jsontab1(j) VALUES ('["a", "b"]')
    *
    ERROR at line 1:
    ORA-02290: check constraint (SYS.JT1ISJ) violated
    

The following two examples shows a row added with valid input :

    
    
    INSERT INTO jsontab1(j) VALUES ('{"a": "a", "b": "b"}');
    
       1 row created.
     
    
    
    INSERT INTO jsontab1(jschd) VALUES (json('"a json string"'));
    
    1 row created.
    

The following example adds another constraint `jschdsv` to table `jsontab1`:

    
    
    ALTER TABLE jsontab1
    ADD jschd JSON CONSTRAINT jschdsv
                       CHECK (jschd IS JSON VALIDATE USING '{"type":"string"}');
    
    Table altered.
    
    
    SQL> INSERT INTO jsontab1(jschd) VALUES (json('3.1415'));
    INSERT INTO jsontab1(jschd) VALUES (json('3.1415'))
    *
    ERROR at line 1:
    ORA-02290: check constraint (SYS.JSCHDSV) violated

IS JSON VALIDATE in WHERE Clause

    
    
    SELECT COUNT(1) FROM jsontab1 WHERE j IS JSON 
    VALIDATE
             '{"type" : "object",
                  "properties" : {
                      "id" : {
                          "type" : "number"
                       }
                   }
               }';

Testing for STRICT or LAX JSON Syntax: Example

The following statement creates table `t` with column `col1`:

    
    
    CREATE TABLE t (col1 VARCHAR2(100));
    

The following statements insert values into column `col1` of table `t`:

    
    
    INSERT INTO t VALUES ( '[ "LIT192", "CS141", "HIS160" ]' );
    INSERT INTO t VALUES ( '{ "Name": "John" }' );
    INSERT INTO t VALUES ( '{ "Grade Values" : { A : 4.0, B : 3.0, C : 2.0 } }');
    INSERT INTO t VALUES ( '{ "isEnrolled" : true }' );
    INSERT INTO t VALUES ( '{ "isMatriculated" : False }' );
    INSERT INTO t VALUES (NULL);
    INSERT INTO t VALUES ('This is not well-formed JSON data');
    

The following statement queries table `t` and returns `col1` values that are
well-formed JSON data. Because neither the `STRICT` nor `LAX` keyword is
specified, this example uses the default `LAX` setting. Therefore, this query
returns values that use strict or lax JSON syntax.

    
    
    SELECT col1
      FROM t
      WHERE col1 IS JSON;
    
    COL1
    --------------------------------------------------
    [ "LIT192", "CS141", "HIS160" ]
    { "Name": "John" }
    { "Grade Values" : { A : 4.0, B : 3.0, C : 2.0 } }
    { "isEnrolled" : true }
    { "isMatriculated" : False }
    

The following statement queries table `t` and returns `col1` values that are
well-formed JSON data. This example specifies the `STRICT` setting. Therefore,
this query returns only values that use strict JSON syntax.

    
    
    SELECT col1
      FROM t
      WHERE col1 IS JSON STRICT;
    
    COL1
    --------------------------------------------------
    [ "LIT192", "CS141", "HIS160" ]
    { "Name": "John" }
    { "isEnrolled" : true }
    

The following statement queries table `t` and returns `col1` values that use
lax JSON syntax, but omits `col1` values that use strict JSON syntax.
Therefore, this query returns only values that contain the exceptions allowed
in lax JSON syntax.

    
    
    SELECT col1
      FROM t
      WHERE col1 IS NOT JSON STRICT AND col1 IS JSON LAX;
    
    COL1
    --------------------------------------------------
    { "Grade Values" : { A : 4.0, B : 3.0, C : 2.0 } }
    { "isMatriculated" : False }

Testing for Unique Keys: Example

The following statement creates table `t` with column `col1`:

    
    
    CREATE TABLE t (col1 VARCHAR2(100));
    

The following statements insert values into column `col1` of table `t`:

    
    
    INSERT INTO t VALUES ('{a:100, b:200, c:300}');
    INSERT INTO t VALUES ('{a:100, a:200, b:300}');
    INSERT INTO t VALUES ('{a:100, b : {a:100, c:300}}');
    

The following statement queries table t and returns `col1` values that are
well-formed JSON data with unique key names within each object:

    
    
    SELECT col1 FROM t
      WHERE col1 IS JSON WITH UNIQUE KEYS;
    
    COL1
    ---------------------------
    {a:100, b:200, c:300}
    {a:100, b : {a:100, c:300}}
    

The second row is returned because, while the key name `a` appears twice, it
is in two different objects.

The following statement queries table `t` and returns `col1` values that are
well-formed JSON data, regardless of whether there are unique key names within
each object:

    
    
    SELECT col1 FROM t
      WHERE col1 IS JSON WITHOUT UNIQUE KEYS;
    
    COL1
    ---------------------------
    {a:100, b:200, c:300}
    {a:100, a:200, b:300}
    {a:100, b : {a:100, c:300}}

Using IS JSON as a Check Constraint: Example

The following statement creates table `j_purchaseorder`, which will store JSON
data in column `po_document`. The statement uses the `IS` `JSON` condition as
a check constraint to ensure that only well-formed JSON is stored in column
`po_document`.

    
    
    CREATE TABLE j_purchaseorder
      (id RAW (16) NOT NULL,
       date_loaded TIMESTAMP(6) WITH TIME ZONE,
       po_document CLOB CONSTRAINT ensure_json CHECK (po_document IS JSON));

See Also:

[Conditions IS JSON and IS NOT
JSON](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADJSN-GUID-8F897ED9-791B-4F53-AFAE-690DE38111D1) of the
JSON Developer's Guide.

### JSON_EQUAL Condition

Syntax

![Description of json_equal_condition.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_equal_condition.gif)  
[Description of the illustration
json_equal_condition.eps](img_text/json_equal_condition.md)

Purpose

The Oracle SQL condition `JSON_EQUAL` compares two `JSON` values and returns
true if they are equal. It returns false if the two values are not equal. The
input values must be valid `JSON` data.

The comparison ignores insignificant whitespace and insignificant object
member order. For example, `JSON` objects are equal, if they have the same
members, regardless of their order.

If either of the two compared inputs has one or more duplicate fields, then
the value returned by `JSON_EQUAL` is unspecified.

`JSON_EQUAL` supports `ERROR ON ERROR`, `FALSE ON ERROR`, and `TRUE ON ERROR`.
The default is `FALSE ON ERROR`. A typical example of an error is when the
input expression is not valid `JSON`.

Examples

The following statements return TRUE:

    
    
    JSON_EQUAL('{}', '{ }')
    
    
    JSON_EQUAL('{a:1, b:2}', '{b:2 , a:1 }')

The following statement return FALSE:

    
    
    JSON_EQUAL('{a:"1"}', '{a:1 }') -> FALSE

The following statement results in a `ORA-40441` `JSON` syntax error

    
    
    JSON_EQUAL('[1]', '[}' ERROR ON ERROR)

See Also:

  * [Oracle Database JSON Developerâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADJSN) for more information. 

### JSON_EXISTS Condition

Use the SQL/JSON condition `JSON_EXISTS` to test whether a specified JSON
value exists in JSON data. This condition returns `TRUE` if the JSON value
exists and `FALSE` if the JSON value does not exist.

JSON_exists_condition::=

![Description of json_exists_condition.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_exists_condition.gif)  
[Description of the illustration
json_exists_condition.eps](img_text/json_exists_condition.md)

(`JSON_basic_path_expression`: See [Oracle Database JSON Developerâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADJSN-GUID-8241AE93-89BE-40E6-89E2-8F9C1A9244F4))

JSON_passing_clause::=

![Description of json_passing_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_passing_clause.gif)  
[Description of the illustration
json_passing_clause.eps](img_text/json_passing_clause.md)

JSON_exists_on_error_clause::=

![Description of json_exists_on_error_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_exists_on_error_clause.gif)  
[Description of the illustration
json_exists_on_error_clause.eps](img_text/json_exists_on_error_clause.md)

JSON_exists_on_empty_clause::=

![Description of json_exists_on_empty_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_exists_on_empty_clause.gif)  
[Description of the illustration
json_exists_on_empty_clause.eps](img_text/json_exists_on_empty_clause.md)

expr

Use this clause to specify the JSON data to be evaluated. For `expr`, specify
an expression that evaluates to a text literal. If `expr` is a column, then
the column must be of data type `VARCHAR2`, `CLOB`, or `BLOB`. If `expr`
evaluates to null or a text literal of length zero, then the condition returns
`UNKNOWN`.

If `expr` is not a text literal of well-formed JSON data using strict or lax
syntax, then the condition returns `FALSE` by default. You can use the
`JSON_exists_on_error_clause` to override this default behavior. Refer to the
[JSON_exists_on_error_clause](SQL-JSON-
Conditions.md#GUID-57762C80-0C8A-4B18-9BA7-9B3F5ABDC988__BABHJEDF).

FORMAT JSON

You must specify `FORMAT` `JSON` if `expr` is a column of data type `BLOB`.

JSON_basic_path_expression

Use this clause to specify a SQL/JSON path expression. The condition uses the
path expression to evaluate `expr` and determine if a JSON value that matches,
or satisfies, the path expression exists. The path expression must be a text
literal, but it can contain variables whose values are passed to the path
expression by the `JSON_passing_clause`. See [Oracle Database JSON
Developerâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADJSN-GUID-7B610884-39CD-4910-85E7-C251D342D879) for the
full semantics of `JSON_basic_path_expression`.

JSON_passing_clause

Use this clause to pass values to the path expression. For `expr`, specify a
value of data type `VARCHAR2`, `NUMBER`, `BINARY_DOUBLE`, `DATE`, `TIMESTAMP`,
or `TIMESTAMP` `WITH` `TIME` `ZONE`. The result of evaluating `expr` is bound
to the corresponding identifier in the `JSON_basic_path_expression`.

JSON_exists_on_error_clause

Use this clause to specify the value returned by this condition when `expr` is
not well-formed JSON data.

You can specify the following clauses:

  * `ERROR` `ON` `ERROR` \- Returns the appropriate Oracle error when `expr` is not well-formed JSON data. 

  * `TRUE` `ON` `ERROR` \- Returns `TRUE` when `expr` is not well-formed JSON data. 

  * `FALSE` `ON` `ERROR` \- Returns `FALSE` when `expr` is not well-formed JSON data. This is the default. 

JSON_exists_on_empty_clause

Use this clause to specify the value returned by this function if no match is
found when the JSON data is evaluated using the SQL/JSON path expression.

You can specify the following clauses:

  * `ERROR` `ON` `EMPTY` \- Returns the appropriate Oracle error when `expr` is not well-formed JSON data.. 

  * `TRUE` `ON` `EMPTY` \- Returns `TRUE` when `expr` is not well-formed JSON data.. 

  * `FALSE` `ON` `EMPTY` \- Returns `FALSE` when expr is not well-formed JSON data. This is the default. . 

Examples

The following statement creates table `t` with column `name`:

    
    
    CREATE TABLE t (name VARCHAR2(100));
    

The following statements insert values into column `name` of table `t`:

    
    
    INSERT INTO t VALUES ('[{first:"John"}, {middle:"Mark"}, {last:"Smith"}]');
    INSERT INTO t VALUES ('[{first:"Mary"}, {last:"Jones"}]');
    INSERT INTO t VALUES ('[{first:"Jeff"}, {last:"Williams"}]');
    INSERT INTO t VALUES ('[{first:"Jean"}, {middle:"Anne"}, {last:"Brown"}]');
    INSERT INTO t VALUES (NULL);
    INSERT INTO t VALUES ('This is not well-formed JSON data');
    

The following statement queries column `name` in table `t` and returns JSON
data that consists of an array whose first element is an object with property
name `first`. The `ON` `ERROR` clause is not specified. Therefore, the
`JSON_EXISTS` condition returns `FALSE` for values that are not well-formed
JSON data.

    
    
    SELECT name FROM t
      WHERE JSON_EXISTS(name, '$[0].first');
    
    NAME
    --------------------------------------------------
    [{first:"John"}, {middle:"Mark"}, {last:"Smith"}]
    [{first:"Mary"}, {last:"Jones"}]
    [{first:"Jeff"}, {last:"Williams"}]
    [{first:"Jean"}, {middle:"Anne"}, {last:"Brown"}]
    

The following statement queries column `name` in table `t` and returns JSON
data that consists of an array whose second element is an object with property
name `middle`. The `ON` `ERROR` clause is not specified. Therefore, the
`JSON_EXISTS` condition returns `FALSE` for values that are not well-formed
JSON data.

    
    
    SELECT name FROM t
      WHERE JSON_EXISTS(name, '$[1].middle');
    
    NAME
    --------------------------------------------------------------------------------
    [{first:"John"}, {middle:"Mark"}, {last:"Smith"}]
    [{first:"Jean"}, {middle:"Anne"}, {last:"Brown"}]
    

The following statement is similar to the previous statement, except that the
`TRUE` `ON` `ERROR` clause is specified. Therefore, the `JSON_EXISTS`
condition returns `TRUE` for values that are not well-formed JSON data.

    
    
    SELECT name FROM t
      WHERE JSON_EXISTS(name, '$[1].middle' TRUE ON ERROR);
    
    NAME
    --------------------------------------------------------------------------------
    [{first:"John"}, {middle:"Mark"}, {last:"Smith"}]
    [{first:"Jean"}, {middle:"Anne"}, {last:"Brown"}]
    This is not well-formed JSON data
    

The following statement queries column `name` in table `t` and returns JSON
data that consists of an array that contains an element that is an object with
property name `last`. The wildcard symbol (`*`) is specified for the array
index. Therefore, the query returns arrays that contain such an object,
regardless of its index number in the array.

    
    
    SELECT name FROM t
      WHERE JSON_EXISTS(name, '$[*].last');
    
    NAME
    --------------------------------------------------
    [{first:"John"}, {middle:"Mark"}, {last:"Smith"}]
    [{first:"Mary"}, {last:"Jones"}]
    [{first:"Jeff"}, {last:"Williams"}]
    [{first:"Jean"}, {middle:"Anne"}, {last:"Brown"}]

The following statement performs a filter expression using the passing clause.
The SQL/JSON variable `$var1` in the comparison predicate` (@.middle ==
$var1)` gets its value from the bind variable `var1` of the PASSING clause.

Using bind variables for value comparisons avoids query re-compilation.

    
    
    SELECT name FROM t
    
      WHERE JSON_EXISTS(name, '$[1]?(@.middle == $var1)' PASSING 'Anne' as "var1");
    
    NAME
    
    --------------------------------------------------------------------------------
    
    [{first:"Jean"}, {middle:"Anne"}, {last:"Brown"}]

See Also:

[Condition JSON_Exists](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADJSN-GUID-8A0043D5-95F8-4918-9126-F86FB0E203F0)

### JSON_TEXTCONTAINS Condition

Use the SQL/JSON condition `JSON_TEXTCONTAINS` to test whether a specified
character string exists in JSON property values. You can use this condition to
filter JSON data on a specific word or number.

This condition takes the following arguments:

  * A table or view column that contains JSON data. A JSON search index, which is an Oracle Text index designed specifically for use with JSON data, must be defined on the column. Each row of JSON data in the column is referred to as a JSON document. 

  * A SQL/JSON path expression. The path expression is applied to each JSON document in an attempt to match a specific JSON object within the document. The path expression can contain only JSON object steps; it cannot contain JSON array steps.

  * A character string. The condition searches for the character string in all of the string and numeric property values in the matched JSON object, including array values. The string must exist as a separate word in the property value. For example, if you search for 'beth', then a match will be found for string property value "beth smith", but not for "elizabeth smith". If you search for '10', then a match will be found for numeric property value 10 or string property value "10 main street", but a match will not be found for numeric property value 110 or string property value "102 main street".

This condition returns `TRUE` if a match is found, and `FALSE` if a match is
not found.

See Also:

[JSON Full text search
queries](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADJSN-GUID-58ADCDE5-7564-4DA0-BED7-B0DBFD5AE6FB)

JSON_textcontains_condition::=

![Description of json_textcontains_condition.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_textcontains_condition.gif)  
[Description of the illustration
json_textcontains_condition.eps](img_text/json_textcontains_condition.md)

(`JSON_basic_path_expression`: See [Oracle Database JSON Developerâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADJSN-GUID-8241AE93-89BE-40E6-89E2-8F9C1A9244F4))

column

Specify the name of the table or view column containing the JSON data to be
tested. The column must be of data type `VARCHAR2`, `CLOB`, or `BLOB`. A JSON
search index, which is an Oracle Text index designed specifically for use with
JSON data, must be defined on the column. If a column value is a null or a
text literal of length zero, then the condition returns `UNKNOWN`.

If a column value is not a text literal of well-formed JSON data using strict
or lax syntax, then the condition returns `FALSE`.

JSON_basic_path_expression

Use this clause to specify a SQL/JSON path expression. The condition uses the
path expression to evaluate `column` and determine if a JSON value that
matches, or satisfies, the path expression exists. The path expression must be
a text literal. See [Oracle Database JSON Developerâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADJSN-GUID-7B610884-39CD-4910-85E7-C251D342D879) for the
full semantics of `JSON_basic_path_expression`.

string

The condition searches for the character string specified by `string`. The
string must be enclosed in single quotation marks.

Examples

The following statement creates table `families` with column `family_doc`:

    
    
    CREATE TABLE families (family_doc VARCHAR2(200));
    

The following statement creates a JSON search index on column `family_doc`:

    
    
    CREATE INDEX ix
      ON families(family_doc)
      INDEXTYPE IS CTXSYS.CONTEXT
      PARAMETERS ('SECTION GROUP CTXSYS.JSON_SECTION_GROUP SYNC (ON COMMIT)');
    

The following statements insert JSON documents that describe families into
column `family_doc`:

    
    
    INSERT INTO families
    VALUES ('{family : {id:10, ages:[40,38,12], address : {street : "10 Main Street"}}}');
    
    INSERT INTO families
    VALUES ('{family : {id:11, ages:[42,40,10,5], address : {street : "200 East Street", apt : 20}}}');
    
    INSERT INTO families
    VALUES ('{family : {id:12, ages:[25,23], address : {street : "300 Oak Street", apt : 10}}}');
    

The following statement commits the transaction:

    
    
    COMMIT;
    

The following query returns the JSON documents that contain `10` in any
property value in the document:

    
    
    SELECT family_doc FROM families
      WHERE JSON_TEXTCONTAINS(family_doc, '$', '10');
    
    FAMILY_DOC
    --------------------------------------------------------------------------------
    {family : {id:10, ages:[40,38,12], address : {street : "10 Main Street"}}}
    {family : {id:11, ages:[42,40,10,5], address : {street : "200 East Street", apt : 20}}}
    {family : {id:12, ages:[25,23], address : {street : "300 Oak Street", apt : 10}}}
    

The following query returns the JSON documents that contain 10 in the `id`
property value:

    
    
    SELECT family_doc FROM families
      where json_textcontains(family_doc, '$.family.id', '10');
    
    FAMILY_DOC
    --------------------------------------------------------------------------------
    {family : {id:10, ages:[40,38,12], address : {street : "10 Main Street"}}}
    

The following query returns the JSON documents that have a 10 in the array of
values for the `ages` property:

    
    
    SELECT family_doc FROM families
      WHERE JSON_TEXTCONTAINS(family_doc, '$.family.ages', '10');
    
    FAMILY_DOC
    --------------------------------------------------------------------------------
    {family : {id:11, ages:[42,40,10,5], address : {street : "200 East Street", apt : 20}}}
    

The following query returns the JSON documents that have a 10 in the `address`
property value:

    
    
    SELECT family_doc FROM families
      WHERE JSON_TEXTCONTAINS(family_doc, '$.family.address', '10');
    
    FAMILY_DOC
    --------------------------------------------------------------------------------
    {family : {id:10, ages:[40,38,12], address : {street : "10 Main Street"}}}
    {family : {id:12, ages:[25,23], address : {street : "300 Oak Street", apt : 10}}}
    

The following query returns the JSON documents that have a 10 in the `apt`
property value:

    
    
    SELECT family_doc FROM families
      WHERE JSON_TEXTCONTAINS(family_doc, '$.family.address.apt', '10');
    
    FAMILY_DOC
    --------------------------------------------------------------------------------
    {family : {id:12, ages:[25,23], address : {street : "300 Oak Street", apt : 10}}}


[← Previous](SQL-JSON-Conditions.md)

[Next →](Compound-Conditions.md)
