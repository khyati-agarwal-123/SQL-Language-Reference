[Previous](TRUNCATE-TABLE.md) [Next](How-to-Read-Syntax-Diagrams.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: MERGE to UPDATE](SQL-Statements-MERGE-to-UPDATE.md)
  3. UPDATE 

## UPDATE

Purpose

Use the `UPDATE` statement to change existing values in a table or in the base
table of a view or the master table of a materialized view.

Prerequisites

For you to update values in a table, the table must be in your own schema or
you must have the `UPDATE` object privilege on the table.

For you to update values in the base table of a view:

  * You must have the `UPDATE` object privilege on the view, and 

  * Whoever owns the schema containing the view must have the `UPDATE` object privilege on the base table. 

The `UPDATE` `ANY` `TABLE` system privilege also allows you to update values
in any table or in the base table of any view.

To update values in an object on a remote database, you must also have the
`READ` or `SELECT` object privilege on the object.

If the `SQL92_SECURITY` initialization parameter is set to `TRUE` and the
`UPDATE` operation references table columns, such as the columns in a
`where_clause`, then you must also have the `SELECT` object privilege on the
object you want to update.

Syntax

update::=

![Description of update.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/update.gif)  
[Description of the illustration update.eps](img_text/update.md)

([DML_table_expression_clause::=](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5__BABGGJCE),
[update_set_clause::=](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5__I2126876),
[where_clause::=](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5__I2126344),
[returning_clause::=](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5__I2126358),
[error_logging_clause::=](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5__BCEEAAGC),
[from_using_clause::=](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5__SECTION_CQ3_4XS_DYB))

DML_table_expression_clause::=

![Description of dml_table_expression_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/dml_table_expression_clause.gif)  
[Description of the illustration
dml_table_expression_clause.eps](img_text/dml_table_expression_clause.md)

([partition_extension_clause::=](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5__CHDBBDEI),
[subquery::=](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2126435)\--part of `SELECT`,
[subquery_restriction_clause::=](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5__I2126407),
[table_collection_expression::=](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5__I2126867))

partition_extension_clause::=

![Description of partition_extension_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/partition_extension_clause.gif)  
[Description of the illustration
partition_extension_clause.eps](img_text/partition_extension_clause.md)

subquery_restriction_clause::=

![Description of subquery_restriction_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/subquery_restriction_clause.gif)  
[Description of the illustration
subquery_restriction_clause.eps](img_text/subquery_restriction_clause.md)

table_collection_expression::=

![Description of table_collection_expression.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/table_collection_expression.gif)  
[Description of the illustration
table_collection_expression.eps](img_text/table_collection_expression.md)

update_set_clause::=

![Description of update_set_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/update_set_clause.gif)  
[Description of the illustration
update_set_clause.eps](img_text/update_set_clause.md)

from_using_clause::=

  

![Description of from_using_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/from_using_clause.gif)  
[Description of the illustration
from_using_clause.eps](img_text/from_using_clause.md)

  

where_clause::=

![Description of where_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/where_clause.gif)  
[Description of the illustration where_clause.eps](img_text/where_clause.md)

order_by_clause::=

See [order_by_clause::=](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056__ORDER_BY_CLAUSE-1E92A06C)

returning_clause::=

![Description of returning_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/returning_clause.gif)  
[Description of the illustration
returning_clause.eps](img_text/returning_clause.md)

error_logging_clause::=

![Description of error_logging_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/error_logging_clause.gif)  
[Description of the illustration
error_logging_clause.eps](img_text/error_logging_clause.md)

Semantics

hint

Specify a comment that passes instructions to the optimizer on choosing an
execution plan for the statement.

You can place a parallel hint immediately after the `UPDATE` keyword to
parallelize both the underlying scan and `UPDATE` operations.

See Also:

  * "[Hints](Comments.md#GUID-D316D545-89E2-4D54-977F-FC97815CD62E)" for the syntax and description of hints 

  * [Oracle Database Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=CNCPT220) for detailed information about parallel execution 

DML_table_expression_clause

The `ONLY` clause applies only to views. Specify `ONLY` syntax if the view in
the `UPDATE` clause is a view that belongs to a hierarchy and you do not want
to update rows from any of its subviews.

See Also:

"[Restrictions on the
DML_table_expression_clause](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5__I2079307)"
and "[Updating a Table:
Examples](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5__I2189758)"

schema

Specify the schema containing the object to be updated. If you omit `schema`,
then the database assumes the object is in your own schema.

table | view | materialized_view |subquery

Specify the name of the table, view, materialized view, or the columns
returned by a subquery to be updated. Issuing an `UPDATE` statement against a
table fires any `UPDATE` triggers associated with the table.

  * If you specify `view`, then the database updates the base table of the view. You cannot update a view except with `INSTEAD` `OF` triggers if the defining query of the view contains one of the following constructs: 

    * A set operator
    * A `DISTINCT` operator 
    * An aggregate or analytic function
    * A `GROUP` `BY`, `ORDER` `BY`, `MODEL`, `CONNECT` `BY`, or `START` `WITH` clause 
    * A collection expression in a `SELECT` list 
    * A subquery in a `SELECT` list 
    * A subquery designated `WITH` `READ` `ONLY`
    * A recursive `WITH` clause 
    * Joins, with some exceptions, as documented in [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN020)
    *   * You cannot update more than one base table through a view.

  * In addition, if the view was created with the `WITH` `CHECK` `OPTION`, then you can update the view only if the resulting data satisfies the view's defining query. 

  * If `table` or the base table of `view` contains one or more domain index columns, then this statement executes the appropriate indextype update routine. 

  * You cannot update rows in a read-only materialized view. If you update rows in a writable materialized view, then the database updates the rows from the underlying container table. However, the updates are overwritten at the next refresh operation. If you update rows in an updatable materialized view that is part of a materialized view group, then the database also updates the corresponding rows in the master table. 

See Also:

  * [Oracle Database Data Cartridge Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADDCI4200) for more information on the indextype update routines 

  * [CREATE MATERIALIZED VIEW](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B) for information on creating updatable materialized views 

partition_extension_clause

Specify the name or partition key value of the partition or subpartition
within `table` targeted for updates. You need not specify the partition name
when updating values in a partitioned table. However in some cases specifying
the partition name can be more efficient than a complicated `where_clause`.

See Also:

"[References to Partitioned Tables and Indexes](Syntax-for-Schema-Objects-and-
Parts-in-SQL-Statements.md#GUID-FED2E424-3F06-4B2B-88D2-DE043CA6E0E4)" and
"[Updating a Partition:
Example](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5__I2130226)"

dblink

Specify a complete or partial name of a database link to a remote database
where the object is located. You can use a database link to update a remote
object only if you are using Oracle Database distributed functionality.

If you omit `dblink,` then the database assumes the object is on the local
database.

Note:

Starting with Oracle Database 12c Release 2 (12.2), the `UPDATE` statement
accepts remote LOB locators as bind variables. Refer to the âDistributed
LOBsâ chapter in [Oracle Database SecureFiles and Large Objects Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADLOB-GUID-7E450E86-3E4E-4714-A164-FD36B93722F6) for more
information.

See Also:

"[References to Objects in Remote Databases](Syntax-for-Schema-Objects-and-
Parts-in-SQL-Statements.md#GUID-61D0B206-A5EA-473F-AD04-7067D6E3914C)" for
information on referring to database links

subquery_restriction_clause

Use the `subquery_restriction_clause` to restrict the subquery in one of the
following ways:

WITH READ ONLY

Specify `WITH READ ONLY` to indicate that the table or view cannot be updated.

WITH CHECK OPTION

Specify `WITH CHECK OPTION` to indicate that Oracle Database prohibits any
changes to the table or view that would produce rows that are not included in
the subquery. When used in the subquery of a DML statement, you can specify
this clause in a subquery in the `FROM` clause but not in subquery in the
`WHERE` clause.

CONSTRAINT constraint

Specify the name of the `CHECK OPTION` constraint. If you omit this
identifier, then Oracle automatically assigns the constraint a name of the
form `SYS_C``n`, where n is an integer that makes the constraint name unique
within the database.

See Also:

"[Using the WITH CHECK OPTION Clause: Example](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2066598)"

table_collection_expression

The `table_collection_expression` lets you inform Oracle that the value of
`collection_expression` should be treated as a table for purposes of query and
DML operations. The `collection_expression` can be a subquery, a column, a
function, or a collection constructor. Regardless of its form, it must return
a collection valueâthat is, a value whose type is nested table or varray.
This process of extracting the elements of a collection is called collection
unnesting.

The optional plus (+) is relevant if you are joining the `TABLE` collection
expression with the parent table. The + creates an outer join of the two, so
that the query returns rows from the outer table even if the collection
expression is null.

Note:

In earlier releases of Oracle, when `collection_expression` was a subquery,
`table_collection_expression` was expressed as `THE` `subquery`. That usage is
now deprecated.

You can use a `table_collection_expression` to update rows in one table based
on rows from another table. For example, you could roll up four quarterly
sales tables into a yearly sales table.

t_alias

Specify a correlation name (alias) for the table, view, or subquery to be
referenced elsewhere in the statement. This alias is required if the
`DML_table_expression_clause` references any object type attributes or object
type methods.

See Also:

"[Correlated Update:
Example](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5__I2068234)"

Restrictions on the DML_table_expression_clause

This clause is subject to the following restrictions:

  * You cannot execute this statement if `table` or the base table of `view` contains any domain indexes marked `IN_PROGRESS` or `FAILED`. 

  * You cannot insert into a partition if any affected index partitions are marked `UNUSABLE`. 

  * You cannot specify the `order_by_clause` in the subquery of the `DML_table_expression_clause`. 

  * If you specify an index, index partition, or index subpartition that has been marked `UNUSABLE`, then the `UPDATE` statement will fail unless the `SKIP_UNUSABLE_INDEXES` session parameter has been set to `TRUE`. 

See Also:

[ALTER SESSION](ALTER-SESSION.md#GUID-27186B28-7EFC-4998-B1ED-2B905CC0211B)
for information on the `SKIP_UNUSABLE_INDEXES` session parameter

update_set_clause

The `update_set_clause` lets you set column values.

column

Specify the name of a column of the object that is to be updated. If you omit
a column of the table from the `update_set_clause`, then the value of that
column remains unchanged.

If `column` refers to a LOB object attribute, then you must first initialize
it with a value of empty or null. You cannot update it with a literal. Also,
if you are updating a LOB value using some method other than a direct `UPDATE`
SQL statement, then you must first lock the row containing the LOB. See
[for_update_clause](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2066346) for more information.

If `column` is a virtual column, you cannot specify it here. Rather, you must
update the values from which the virtual column is derived.

If `column` is part of the partitioning key of a partitioned table, then
`UPDATE` will fail if you change a value in the column that would move the row
to a different partition or subpartition, unless you enable row movement.
Refer to the `row_movement_clause` of [CREATE TABLE](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6) or [ALTER TABLE](ALTER-
TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877).

In addition, if `column` is part of the partitioning key of a list-partitioned
table, then `UPDATE` will fail if you specify a value for the column that does
not already exist in the `partition_key_value` list of one of the partitions.

subquery

Specify a subquery that returns exactly one row for each row updated.

  * If you specify only one column in the `update_set_clause`, then the subquery can return only one value. 

  * If you specify multiple columns in the `update_set_clause`, then the subquery must return as many values as you have specified columns. 

  * If the subquery returns no rows, then the column is assigned a null. 

  * If this `subquery` refers to remote objects, then the `UPDATE` operation can run in parallel as long as the reference does not loop back to an object on the local database. However, if the `subquery` in the `DML_table_expression_clause` refers to any remote objects, then the `UPDATE` operation will run serially without notification. 

You can use the `flashback_query_clause` within the subquery to update `table`
with past data. Refer to the [flashback_query_clause](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2112818) of `SELECT` for more
information on this clause.

See Also:

  * [SELECT](SELECT.md#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6) and "[Using Subqueries](Using-Subqueries.md#GUID-53A705B6-0358-4E2B-92ED-A83DE83DFD20)"

  * [parallel_clause](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__CJACIHHF) in the [CREATE TABLE](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6) documentation 

expr

Specify an expression that resolves to the new value assigned to the
corresponding column.

Note:

[Expressions](Expressions.md#GUID-E7A5363C-AEE9-4809-99C1-1A9C6E3AE017) for
the syntax of `expr` and "[Updating an Object Table:
Example](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5__I2135485)"

DEFAULT

Specify `DEFAULT` to set the column to the value previously specified as the
default value for the column. If no default value for the corresponding column
has been specified, then the database sets the column to null.

Restriction on Updating to Default Values

You cannot specify `DEFAULT` if you are updating a view.

You cannot use the `DEFAULT` clause in an `UPDATE` statement if the table that
you are specifying has an Oracle Label Security policy enabled.

VALUE Clause

The `VALUE` clause lets you specify the entire row of an object table.

Restriction on the VALUE clause

You can specify this clause only for an object table.

Note:

If you insert string literals into a `RAW` column, then during subsequent
queries, Oracle Database will perform a full table scan rather than using any
index that might exist on the `RAW` column.

See Also:

"[Updating an Object Table:
Example](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5__I2135485)"

from_using_clause

Use this clause to filter the rows `UPDATE` changes, or to provide the values
for the columns in the target table. Specify the join conditions in the
`where_clause`. You can outer join source tables to the target table with (+).
The target table cannot be the outer table in the join.

You can join many tables, views, and inline views. Specify the join conditions
in the `where_clause` or use the `join_clause` to join these to each other
with ANSI join syntax.

You can specify the same table in the `dml_table_expression_clause` and
`from_clause`. When you do so they must have unique aliases.

Example: Update With Direct-Join

In this example, the join condition between table employees `e` and table jobs
`j` determines which rows of employees are updated. The column
`jobs.max_salary` supplies the new values for `employees.salary`:

    
    
    UPDATE employees e  
    SET    e.salary = j.max_salary
    FROM   jobs j
    WHERE  j.job_id = e.job_id;
    

Direct joins for `UPDATE` have the same semantics and restrictions as `SELECT`
in the `from_clause` and `where_clause`. The target table has the same
restrictions as `UPDATE`. Triggers on the target table fire as normal.

Restrictions

  * You cannot specify ANSI join syntax involving the `dml_table_expression_clause`. However, ANSI join syntax is allowed between the tables specified in the `FROM` clause. Right and full outer joins are not allowed. 

  * The `UPDATE` can change each row at most once. If the join condition results in the same row being updated more than once, the statement will raise an `ORA-30926` error. 

  * You can only specify one table, view, or materialized view in `dml_table_expression_clause` when the `from_clause` is present. 

  * The left-hand side of `update_set_clause` must be a column from the` dml_table_expression_clause` and not from the `from_clause`. 

  * You can use a lateral view in the `FROM` clause, but it cannot reference a column from the update target. It may be outer-joined. 

  * Order by position is not allowed in the `order_by_clause`. 

  * `UPDATE` with `from_clause` supports `returning_clause` and `error_logging_clause`. 

  * Hint clause can be used to specify instructions to the optimizer for joins involving the `from_clause`. 

where_clause

The `where_clause` lets you restrict the rows updated to those for which the
specified `condition` is true. If you omit this clause, then the database
updates all rows in the table or view. Refer to
[Conditions](Conditions.md#GUID-C2E3ED44-16E7-4924-9125-E1693B1022A8) for
the syntax of `condition`.

The `where_clause` determines the rows in which values are updated. If you do
not specify the `where_clause`, then all rows are updated. For each row that
satisfies the `where_clause`, the columns to the left of the equality operator
(=) in the `update_set_clause` are set to the values of the corresponding
expressions to the right of the operator. The expressions are evaluated as the
row is updated.

order_by_clause

The following restrictions apply to the `ORDER BY` clause:

  * When used in an analytic function, the `order_by_clause` must take an expression `expr`. 
  * The `SIBLINGS` keyword is not valid (it is relevant only in hierarchical queries) 

  * The `position` alias is invalid. 

See [order_by_clause ](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056__GUID-666C34CD-99A1-4974-A898-AD1ACD8CA42E)

returning_clause

You can specify this clause for tables, views, and materialized views with a
single base table.

When operating on a single row, a DML statement with a `returning_clause` can
retrieve column values using the affected row, rowid, and `REFs` to the
affected row and store them in host variables or PL/SQL variables.

When operating on multiple rows, a DML statement with the `returning_clause`
returns values from expressions, rowids, and `REFs` involving the affected
rows in bind arrays.

expr

Each item in the `expr` list must be a valid expression syntax.

INTO

The `INTO` clause indicates that the values of the changed rows are to be
stored in the variable(s) specified in `data_item` list.

data_item

Each `data_item` is a host variable or PL/SQL variable that stores the
retrieved `expr` value.

For each expression in the `RETURNING` list, you must specify a corresponding
type-compatible PL/SQL variable or host variable in the `INTO` list.

Given columns `c1` and `c2` in a table, you can specify `OLD` for a column
`c1`, (for example `OLD c1`). You can also specify `OLD` for a column
referenced by a column expression (for example `c1+OLD c2`). When `OLD` is
specified for a column, the column value before the update is returned. In the
case of a column referenced by a column expression, what is returned is the
result from evaluating the column expression using the column value before the
update.

`NEW` can be explicitly specified for a column, or column referenced in an
expression to return a column value after the update, or an expression result
that uses the after update value of a column.

When `OLD` and `NEW` are both omitted for a column or an expression, the after
update column value, or expression result computed using after update column
values, is returned.

Restrictions

The following restrictions apply to the `RETURNING` clause:

  * The `expr` is restricted as follows: 

    * For `UPDATE` and `DELETE` statements each `expr` must be a simple expression or a single-set aggregate function expression. You cannot combine simple expressions and single-set aggregate function expressions in the same `returning_clause`. For `INSERT` statements, each `expr` must be a simple expression. Aggregate functions are not supported in an `INSERT` statement `RETURNING` clause. 

    * Single-set aggregate function expressions cannot include the `DISTINCT` keyword. 

  * If the `expr` list contains a primary key column or other `NOT` `NULL` column, then the update statement fails if the table has a `BEFORE` `UPDATE` trigger defined on it. 

  * You cannot specify the `returning_clause` for a multitable insert. 

  * You cannot use this clause with parallel DML or with remote objects.

  * You cannot retrieve `LONG` types with this clause. 

  * You cannot specify this clause for a view on which an `INSTEAD` `OF` trigger has been defined. 

See Also:

[Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS012) for information on using the `BULK` `COLLECT`
clause to return multiple values to collection variables

error_logging_clause

The `error_logging_clause` has the same behavior in an `UPDATE` statement as
it does in an `INSERT` statement. Refer to the `INSERT` statement
[error_logging_clause](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__BGBEIACB)
for more information.

See Also:

"[Inserting Into a Table with Error Logging:
Example](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__BCEGDJDJ)"

Examples

Updating a Table: Examples

The following statement gives null commissions to all employees with the job
`SH_CLERK`:

    
    
    UPDATE employees
       SET commission_pct = NULL
       WHERE job_id = 'SH_CLERK';
    

The following statement promotes Douglas Grant to manager of Department 20
with a $1,000 raise:

    
    
    UPDATE employees SET 
        job_id = 'SA_MAN', salary = salary + 1000, department_id = 120 
        WHERE first_name||' '||last_name = 'Douglas Grant'; 
    

The following statement increases the salary of an employee in the `employees`
table on the `remote` database:

    
    
    UPDATE employees@remote
       SET salary = salary*1.1
       WHERE last_name = 'Baer';
    

The next example shows the following syntactic constructs of the `UPDATE`
statement:

  * Both forms of the `update_set_clause` together in a single statement 

  * A correlated subquery 

  * A `where_clause` to limit the updated rows 

    
    
    UPDATE employees a 
        SET department_id = 
            (SELECT department_id 
                FROM departments 
                WHERE location_id = '2100'), 
            (salary, commission_pct) = 
            (SELECT 1.1*AVG(salary), 1.5*AVG(commission_pct) 
              FROM employees b 
              WHERE a.department_id = b.department_id) 
        WHERE department_id IN 
            (SELECT department_id 
              FROM departments
              WHERE location_id = 2900 
                  OR location_id = 2700); 
    

The preceding `UPDATE` statement performs the following operations:

  * Updates only those employees who work in Geneva or Munich (locations 2900 and 2700) 

  * Sets `department_id` for these employees to the `department_id` corresponding to Bombay (`location_id` 2100) 

  * Sets each employee's salary to 1.1 times the average salary of their department 

  * Sets each employee's commission to 1.5 times the average commission of their department 

Updating a Partition: Example

The following example updates values in a single partition of the `sales`
table:

    
    
    UPDATE sales PARTITION (sales_q1_1999) s
       SET s.promo_id = 494
       WHERE amount_sold > 1000;

Updating an Object Table: Example

The following statement creates two object tables, `people_demo1` and
`people_demo2`, of the `people_typ` object created in [Table Collections:
Examples](SELECT.md#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6__I2071643).
The example shows how to update a row of `people_demo1` by selecting a row
from `people_demo2`:

    
    
    CREATE TABLE people_demo1 OF people_typ;
    
    CREATE TABLE people_demo2 OF people_typ;
    
    UPDATE people_demo1 p SET VALUE(p) =
       (SELECT VALUE(q) FROM people_demo2 q
        WHERE p.department_id = q.department_id)
       WHERE p.department_id = 10;
    

The example uses the `VALUE` object reference function in both the `SET`
clause and the subquery.

Correlated Update: Example

For an example that uses a correlated subquery to update nested table rows,
refer to "[Table Collections: Examples](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2071643)".

Using the RETURNING Clause During UPDATE: Example

The following example returns values from the updated row and stores the
result in PL/SQL variables `bnd1`, `bnd2`, `bnd3`:

    
    
    UPDATE employees
      SET job_id ='SA_MAN', salary = salary + 1000, department_id = 140
      WHERE last_name = 'Jones'
      RETURNING salary*0.25, last_name, department_id
        INTO :bnd1, :bnd2, :bnd3;
    

The following example shows that you can specify a single-set aggregate
function in the expression of the returning clause:

    
    
    UPDATE employees
       SET salary = salary * 1.1
       WHERE department_id = 100
       RETURNING SUM(salary) INTO :bnd1;

Update Using Direct Join: Example

The following example sets every employee's salary to the max salary for their
job:

    
    
    UPDATE hr.employees e
        SET e.salary = j.max_salary
        FROM hr.jobs j    
        WHERE e.job_id = j.job_id;


[← Previous](TRUNCATE-TABLE.md)

[Next →](How-to-Read-Syntax-Diagrams.md)
