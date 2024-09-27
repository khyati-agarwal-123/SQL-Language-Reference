[Previous](JSON_TABLE.md) [Next](JSON_VALUE.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. JSON_TRANSFORM

## JSON_TRANSFORM

Syntax

  

![Description of json_transform.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_transform.gif)  
[Description of the illustration
json_transform.eps](img_text/json_transform.md)

  

([operation::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-D5868C5C-960B-4C87-89D4-C8B077F9B3BB),
[JSON_TRANSFORM_returning_clause::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-66E4F03C-9497-4508-B791-E07AE23CEE73),
[JSON_passing_clause::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-05C58A2A-BA46-4BCB-AFBF-
FEF4C23B411C) )

JSON_TRANSFORM_returning_clause::=

![Description of json_transform_returning_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_transform_returning_clause.gif)  
[Description of the illustration
json_transform_returning_clause.eps](img_text/json_transform_returning_clause.md)

JSON_passing_clause::=

For details on `JSON_passing_clause` see [JSON_EXISTS Condition](SQL-JSON-
Conditions.md#GUID-57762C80-0C8A-4B18-9BA7-9B3F5ABDC988).

operation ::=

![Description of operation.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/operation.gif)  
[Description of the illustration operation.eps](img_text/operation.md)

([append_op::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-3BE6A643-EB1D-457B-B4EF-F08BB2AAF385),
[case_op::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-56923EE2-8781-455A-B7DE-F4055B5215C2),[copy_op::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-854F592D-A0E8-4E6D-8388-C9E289225828),[insert_op::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-
DC01CB2E-9330-4164-8A46-1956D66DBE14),[intersect_op::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-
ADE2FECD-42F4-4394-8BC1-F2D49DB32D75),[keep_op::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-3C13BF39-A58B-4138-BFFC-17FE7BEA1744),[merge_op::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-06E6269F-311E-487A-919C-46E7E29EC06E),[minus_op::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-57FBD245-2866-4722-996A-E0D843C2BA56),[nested_path_op::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-B26F29BD-54A7-4440-9CE5-938A3922233A),[prepend_op::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-A8D09779-42FA-4347-B3E2-C02145FDC270),[remove_op::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-3D372EA3-BC81-4179-BA04-9F84C813B2EF),[rename_op::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-C95B75F6-6702-425A-B4A8-EB01F5105545),[replace_op::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-5C19B9A0-9796-46D4-9DE6-452665DFA54C),[set_op](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-3CBB7957-C794-477F-883E-6070E8908067),[sort_op](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-4C64E47C-91AA-472B-B94A-FD2BAAAFD9EB),[union_op](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-035E9FDC-
EB31-4DC8-81F4-835311BD4EA2),)

append_op ::=

  

![Description of append_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/append_op.gif)  
[Description of the illustration append_op.eps](img_text/append_op.md)

  

[rhs_expr::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-1BBA7230-9695-482E-B686-BADB0724F307)

case_op::=

  

![Description of case_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/case_op.gif)  
[Description of the illustration case_op.eps](img_text/case_op.md)

  

copy_op::=

  

![Description of copy_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/copy_op.gif)  
[Description of the illustration copy_op.eps](img_text/copy_op.md)

  

[rhs_expr::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-1BBA7230-9695-482E-B686-BADB0724F307)

insert_op ::=

  

![Description of insert_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/insert_op.gif)  
[Description of the illustration insert_op.eps](img_text/insert_op.md)

  

[rhs_expr::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-1BBA7230-9695-482E-B686-BADB0724F307)

intersect_op::=

  

![Description of intersect_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/intersect_op.gif)  
[Description of the illustration intersect_op.eps](img_text/intersect_op.md)

  

[rhs_expr::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-1BBA7230-9695-482E-B686-BADB0724F307)

keep_op ::=

  

![Description of keep_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/keep_op.gif)  
[Description of the illustration keep_op.eps](img_text/keep_op.md)

  

merge_op::=

  

![Description of merge_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/merge_op.gif)  
[Description of the illustration merge_op.eps](img_text/merge_op.md)

  

[rhs_expr::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-1BBA7230-9695-482E-B686-BADB0724F307)

minus_op::=

  

![Description of minus_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/minus_op.gif)  
[Description of the illustration minus_op.eps](img_text/minus_op.md)

  

[rhs_expr::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-1BBA7230-9695-482E-B686-BADB0724F307)

nested_path_op::=

![Description of nested_path_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/nested_path_op.gif)  
[Description of the illustration
nested_path_op.eps](img_text/nested_path_op.md)

prepend_op::=

  

![Description of prepend_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/prepend_op.gif)  
[Description of the illustration prepend_op.eps](img_text/prepend_op.md)

  

[rhs_expr::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-1BBA7230-9695-482E-B686-BADB0724F307)

remove_op ::=

  

![Description of remove_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/remove_op.gif)  
[Description of the illustration remove_op.eps](img_text/remove_op.md)

  

rename_op ::=

  

![Description of rename_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/rename_op.gif)  
[Description of the illustration rename_op.eps](img_text/rename_op.md)

  

replace_op ::=

  

![Description of replace_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/replace_op.gif)  
[Description of the illustration replace_op.eps](img_text/replace_op.md)

  

[rhs_expr::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-1BBA7230-9695-482E-B686-BADB0724F307)

set_op ::=

  

![Description of set_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/set_op.gif)  
[Description of the illustration set_op.eps](img_text/set_op.md)

  

[rhs_expr::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-1BBA7230-9695-482E-B686-BADB0724F307)

sort_op::=

![Description of sort_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/sort_op.gif)  
[Description of the illustration sort_op.eps](img_text/sort_op.md)

union_op::=

  

![Description of union_op.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/union_op.gif)  
[Description of the illustration union_op.eps](img_text/union_op.md)

  

[rhs_expr::=](JSON_TRANSFORM.md#GUID-
DD2A821B-C688-4310-81B5-5F45090B9366__GUID-1BBA7230-9695-482E-B686-BADB0724F307)

rhs_expr ::=

  

![Description of rhs_expr.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/rhs_expr.gif)  
[Description of the illustration rhs_expr.eps](img_text/rhs_expr.md)

  

Purpose

`JSON_TRANSFORM` modifies JSON documents. You specify operations to perform
and SQL/JSON path expressions that target the places to modify. The operations
are applied to the input data in the order specified: each operation acts on
the data that results from applying all of the preceding operations.

`JSON_TRANSFORM` either succeeds completely or not at all. If any of the
specified operations raises an error, then none of the operations take effect.
`JSON_TRANSFORM` returns the original data changed according to the operations
specified.

You can use the `JSON_TRANSFORM` within the `UPDATE` statement to modify
documents in a JSON column.

You can use it in a `SELECT` list, to modify the selected documents. The
modified documents can be returned or processed further.

`JSON_TRANSFORM` can accept as input, and return as output, any SQL data type
that supports JSON data: `JSON`, `VARCHAR2`, `CLOB`, or `BLOB`. Note that data
type `JSON` is available only if database initialization parameter compatible
is 20 or greater.

The default return (output) data type is the same as the input data type.

See Also:

[Oracle SQL Function
JSON_TRANSFORM](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADJSN-GUID-7BED994B-EAA3-4FF0-824D-C12ADAB862C1) of the
JSON Developer's Guide for a full discussion with examples.

JSON_TRANSFORM Operations

  * Use `APPEND` to append the values that are specified by the RHS to the array that is targeted by the LHS path expression. 

`APPEND` has the effect of `INSERT` for an array position of last+1.

An error is raised if the LHS path expression targets an existing field whose
value is not an array.

If the RHS targets an array then the LHS array is updated by appending the
elements of the RHS array to it, in order.

  * Use `CASE` to set conditions to perform a sequence of `JSON_TRANSFORM` operations. 

This is a control operation that conditionally applies other operations, which
in turn can modify data.

The syntax is keyword `CASE` followed by one or more `WHEN` clauses, followed
optionally by an `ELSE` clause, followed by `END`.

A `WHEN` clause is keyword `WHEN` followed by a path expression, followed by a
`THEN` clause.

The path expression contains a filter condition, which checks for the
existence of some data.

A `THEN` or an `ELSE` clause is keyword `THEN` or `ELSE`, respectively,
followed by parentheses (()) containing zero or more `JSON_TRANSFORM`
operations.

The operations of a `THEN` clause are performed if the condition of its `WHEN`
clause is satisfied. The operations of the optional `ELSE` clause are
performed if the condition of no `WHEN` clause is satisfied.

The syntax of the `JSON_TRANSFORM` `CASE` operation is thus essentially the
same as an Oracle SQL searched `CASE` expression, except that it is the
predicate that is tested and the resulting effect of each `THEN`/`ELSE`
branch.

For SQL, the predicate tested is a SQL comparison. For `JSON_TRANSFORM`, the
predicate is a path expression that checks for the existence of some data.
(The check is essentially done using `JSON_EXISTS`.)

For SQL, each `THEN`/`ELSE` branch holds a SQL expression to evaluate, and its
value is returned as the result of the `CASE` expression. For json_transform,
each `THEN`/`ELSE` branch holds a (parenthesized) sequence of `JSON_TRANSFORM`
operations, which are performed in order.

The conditional path expressions of the `WHEN` clauses are tested in order,
until one succeeds (those that follow are not tested). The `THEN` operations
for the successful `WHEN` test are then performed, in order.

  * Use `COPY` to replace the elements of the array that is targeted by the LHS path expression with the values that are specified by the RHS. An error is raised if the LHS path expression does not target an array. The operation can accept a sequence of multiple values matched by the RHS path expression. 

  * `INSERT` Insert the value of the specified SQL expression at the location that's targeted by the specified path expression that follows the equal sign (=), which must be either the field of an object or an array position (otherwise, an error is raised). By default, an error is raised if a targeted object field already exists. 

`INSERT` for an object field has the effect of `SET` with clause `CREATE ON
MISSING `(default for `SET`), except that the default behavior for `ON
EXISTING` is `ERROR`, not `REPLACE`.)

You can specify an array position past the current end of an array. In that
case, the array is lengthened to accommodate insertion of the value at the
indicated position, and the intervening positions are filled with JSON null
values.

For example, if the input JSON data is `{"a":["b"]}` then `INSERT '$.a[3]'=42`
returns `{"a":["b", null, null 42]}` as the modified data. The elements at
array positions 1 and 2 are null.

  * Use `INTERSECT` to remove all elements of the array that is targeted by the LHS path expression that are not equal to any value specified by the RHS. Remove any duplicate elements. Note that this is a set operation. The order of all array elements is undefined after the operation. 

  * Use `MERGE` to add specified fields (name and value) matched by the RHS path expression to the object that is targeted by the LHS path expression. Ignore any fields specified by the RHS that are already in the targeted LHS object. If the same field is specified more than once by the RHS then use only the last one in the sequence of matches. 

  * Use `MINUS` to remove all elements of the array that is targeted by the LHS path expression that are equal to a value specified by the RHS. Remove any duplicate elements. Note that this is a set operation. The order of all array elements is undefined after the operation. 

  * `KEEP` removes all parts of the input data that are not targeted by at least one of the specified path expressions. A topmost object or array is not removed, it is emptied and becomes an empty object ({}) or array ([]). 

  * Use `NESTED PATH` to define a scope (a particular part of your data) in which to apply a sequence of operations. 

  * Use `PREPEND` to prepend the values that are specified by the RHS to the array that is targeted by the LHS path expression. The operation can accept a sequence of multiple values matched by the RHS path expression. 

An error is raised if the LHS path expression targets an existing field whose
value is not an array.

When prepending a single value, `PREPEND` has the effect of `INSERT` for an
array position of 0.

If the RHS targets an array then the LHS array is updated by prepending the
elements of the RHS array to it, in order.

  * `REMOVE` Remove the input data that's targeted by the specified path expression. An error is raised if you try to remove all of the data, for example you cannot use `REMOVE '$'`. By default, no error is raised if the targeted data does not exist (`IGNORE ON MISSING`). 

  * `RENAME` renames the field that is targeted by the specified path expression to the value of the SQL expression that follows the equal sign (=). By default, no error is raised if the targeted field does not exist (`IGNORE ON MISSING`). 

  * `REPLACE` replaces the data that's targeted by the specified path expression with the value of the specified SQL expression that follows the equal sign (=). By default, no error is raised if the targeted data does not exist (`IGNORE ON MISSING`). 

`REPLACE` has the effect of `SET` with clause `IGNORE ON MISSING`.

  * `SET` Set what the LHS specifies to the value specified by what follows the equal sign (=). The LHS can be either a SQL/JSON variable or a path expression that targets data. If the RHS is a SQL expression then its value is assigned to the LHS variable. When the LHS specifies a path expression, the default behavior is to replace existing targeted data with the new value, or insert the new value at the targeted location if the path expression matches nothing. (See operator `INSERT` about inserting an array element past the end of the array.) 

  * When the LHS specifies a SQL/JSON variable, the variable is dynamically assigned to whatever is specified by the RHS. (The variable is created if it does not yet exist.) The variable continues to have that value until it is set to a different value by a subsequent `SET` operation (in the same `JSON_TRANSFORM` invocation). 

If the RHS is a path expression then its targeted data is assigned to the
variable.

Setting a variable is a control operation; it can affect how subsequent
operations modify data, but it does not, itself, directly modify data.

When the LHS specifies a path expression, the default behavior is like that of
SQL `UPSERT`: replace existing targeted data with the new value, or insert the
new value at the targeted location if the path expression matches nothing.
(See operator `INSERT` about inserting an array element past the end of the
array.)

  * `SORT` sorts the elements of the array targeted by the specified path. The result includes all elements of the array (none are dropped); the only possible change is that they are reordered. 

  * Use `UNION` to add the values specified by the RHS to the array that is targeted by the LHS path expression. Remove any duplicate elements. The operation can accept a sequence of multiple values matched by the RHS path expression. Note that this is a set operation. The order of all array elements is undefined after the operation. 

JSON_TRANSFORM_returning_clause

After you specify the operations you can use `JSON_TRANSFORM_returning_clause`
to specify the return data type.

JSON_passing_clause

You can use `JSON_passing_clause` to specify SQL bindings of bind variables to
SQL/JSON variables similar to the `JSON_EXISTS` condition and the SQL/JSON
query functions.

Examples

Example 1 : Update a JSON Column with a Timestamp

    
    
    UPDATE t SET jcol = JSON_TRANSFORM(jcol, SET '$.lastUpdated' = SYSTIMESTAMP)

Example 2 : Remove a Social Security Number before Shipping JSON to a Client

    
    
    SELECT JSON_TRANSFORM (jcol, REMOVE '$.ssn') FROM t WHERE â¦

JSON_TRANSFORM_returning_clause

If the input data is JSON, then the output data type is also JSON. For all
other input types, the default output data type is `VARCHAR2(4000)`.


[← Previous](JSON_TABLE.md)

[Next →](JSON_VALUE.md)
