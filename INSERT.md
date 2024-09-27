[Previous](GRANT.md) [Next](LOCK-TABLE.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: DROP TABLE to LOCK TABLE](SQL-Statements-DROP-TABLE-to-LOCK-TABLE.md)
  3. INSERT 

## INSERT

Purpose

Use the `INSERT` statement to add rows to a table, the base table of a view, a
partition of a partitioned table or a subpartition of a composite-partitioned
table, or an object table or the base table of an object view.

Prerequisites

For you to insert rows into a table, the table must be in your own schema or
you must have the `INSERT` object privilege on the table.

For you to insert rows into the base table of a view, the owner of the schema
containing the view must have the `INSERT` object privilege on the base table.
Also, if the view is in a schema other than your own, then you must have the
`INSERT` object privilege on the view.

If you have the `INSERT` `ANY` `TABLE` system privilege, then you can also
insert rows into any table or the base table of any view.

You must also have the `READ` or `SELECT` object privilege on the table into
which you want to insert rows if the table is on a remote database.

Conventional and Direct-Path INSERT

You can use the `INSERT` statement to insert data into a table, partition, or
view in two ways: conventional `INSERT` and direct-path `INSERT`. When you
issue a conventional `INSERT` statement, Oracle Database reuses free space in
the table into which you are inserting and maintains referential integrity
constraints. With direct-path `INSERT`, the database appends the inserted data
after existing data in the table. Data is written directly into data files,
bypassing the buffer cache. Free space in the existing data is not reused.
This alternative enhances performance during insert operations and is similar
to the functionality of the Oracle direct-path loader utility, SQL*Loader.
When you insert into a table that has been created in parallel mode, direct-
path `INSERT` is the default.

The manner in which the database generates redo and undo data depends in part
on whether you are using conventional or direct-path `INSERT`:

  * Conventional `INSERT` always generates maximal redo and undo for changes to both data and metadata, regardless of the logging setting of the table and the archivelog and force logging settings of the database. 

  * Direct-path `INSERT` generates both redo and undo for metadata changes, because these are needed for operation recovery. For data changes, undo and redo are generated as follows: 

    * Direct-path `INSERT` always bypasses undo generation for data changes. 

    * If the database is not in `ARCHIVELOG` or `FORCE` `LOGGING` mode, then no redo is generated for data changes, regardless of the logging setting of the table. 

    * If the database is in `ARCHIVELOG` mode (but not in `FORCE` `LOGGING` mode), then direct-path `INSERT` generates data redo for `LOGGING` tables but not for `NOLOGGING` tables. 

    * If the database is in `ARCHIVELOG` and `FORCE` `LOGGING` mode, then direct-path SQL generate data redo for both `LOGGING` and `NOLOGGING` tables. 

Direct-path `INSERT` is subject to a number of restrictions. If any of these
restrictions is violated, then Oracle Database executes conventional `INSERT`
serially without returning any message, unless otherwise noted:

  * You can have multiple direct-path `INSERT` statements in a single transaction, with or without other DML statements. However, after one DML statement alters a particular table, partition, or index, no other DML statement in the transaction can access that table, partition, or index. 

  * Queries that access the same table, partition, or index are allowed before the direct-path `INSERT` statement, but not after it. 

  * If any serial or parallel statement attempts to access a table that has already been modified by a direct-path `INSERT` in the same transaction, then the database returns an error and rejects the statement. 

  * The target table cannot be of a cluster.

  * The target table cannot contain object type columns.

  * Direct-path `INSERT` is not supported for an index-organized table (IOT) if it has a mapping table, or if it is reference by a materialized view. 

  * Direct-path `INSERT` into a single partition of an index-organized table (IOT), into a partitioned IOT with only one partition, or into an IOT that is not partitioned, will be done serially, even if the IOT was created in parallel mode or you specify the `APPEND` or `APPEND_VALUES` hint. However, direct-path `INSERT` operations into a partitioned IOT will honor parallel mode as long as the partition-extended name is not used and the IOT has more than one partition. 

  * The target table cannot have any triggers or referential integrity constraints defined on it.

  * The target table cannot be replicated.

  * A transaction containing a direct-path `INSERT` statement cannot be or become distributed. 

See Also:

  * [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN01509) for a more complete description of direct-path `INSERT`

  * [Oracle Database Utilities](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=SUTIL003) for information on SQL*Loader 

  * [Oracle Database SQL Tuning Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=TGSQL344) for information on statistics gathering when inserting into an empty table using direct-path `INSERT`

Syntax

insert::=

![Description of insert.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/insert.gif)  
[Description of the illustration insert.eps](img_text/insert.md)

([single_table_insert::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2121671),
[multi_table_insert::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2121682))

single_table_insert::=

![Description of single_table_insert.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/single_table_insert.gif)  
[Description of the illustration
single_table_insert.eps](img_text/single_table_insert.md)

([insert_into_clause::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2121694),
[insert_values_clause::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2122346),
[returning_clause::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2122356),
[subquery::=](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2126435),
[error_logging_clause::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__BGBDIGAH))

insert_into_clause::=

![Description of insert_into_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/insert_into_clause.gif)  
[Description of the illustration
insert_into_clause.eps](img_text/insert_into_clause.md)

([DML_table_expression_clause::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2126242))

insert_values_clause::=

  

![Description of insert_values_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/insert_values_clause.gif)  
[Description of the illustration
insert_values_clause.eps](img_text/insert_values_clause.md)

  

returning_clause::=

![Description of returning_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/returning_clause.gif)  
[Description of the illustration
returning_clause.eps](img_text/returning_clause.md)

multi_table_insert::=

![Description of multi_table_insert.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/multi_table_insert.gif)  
[Description of the illustration
multi_table_insert.eps](img_text/multi_table_insert.md)

([insert_into_clause::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2121694),
[insert_values_clause::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2122346),
[conditional_insert_clause::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2121821),
[subquery::=](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2126435),
[error_logging_clause::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__BGBDIGAH))

conditional_insert_clause::=

![Description of conditional_insert_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/conditional_insert_clause.gif)  
[Description of the illustration
conditional_insert_clause.eps](img_text/conditional_insert_clause.md)

([insert_into_clause::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2121694),
[insert_values_clause::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2122346))

DML_table_expression_clause::=

![Description of dml_table_expression_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/dml_table_expression_clause.gif)  
[Description of the illustration
dml_table_expression_clause.eps](img_text/dml_table_expression_clause.md)

([partition_extension_clause::=](LOCK-TABLE.md#GUID-4C00C6D9-C5C5-46CC-
AD33-A64001744A4C__BABBDIIJ), [subquery::=](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2126435)âpart of `SELECT`,
[subquery_restriction_clause::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2121860),
[table_collection_expression::=](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2121871))

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

error_logging_clause::=

![Description of error_logging_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/error_logging_clause.gif)  
[Description of the illustration
error_logging_clause.eps](img_text/error_logging_clause.md)

Semantics

hint

Specify a comment that passes instructions to the optimizer on choosing an
execution plan for the statement.

For a multi-table insert, if you specify the `PARALLEL` hint for any target
table, then the entire multi-table insert statement is parallelized even if
the target tables have not been created or altered with `PARALLEL` specified.
If you do not specify the `PARALLEL` hint, then the insert operation will not
be parallelized unless all target tables were created or altered with
`PARALLEL` specified.

See Also:

  * "[Hints](Comments.md#GUID-D316D545-89E2-4D54-977F-FC97815CD62E)" for the syntax and description of hints 

  * "[Restrictions on Multi-Table Inserts](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2080134)"

single_table_insert

In a single-table insert, you insert values into one row of a table, view, or
materialized view by specifying values explicitly or by retrieving the values
through a subquery.

You can use the `flashback_query_clause` in `subquery` to insert past data
into `table`. Refer to the [flashback_query_clause](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2112818) of `SELECT` for more
information on this clause.

Restriction on Single-Table Inserts

If you retrieve values through a subquery, then the select list of the
subquery must have the same number of columns as the column list of the
`INSERT` statement. If you omit the column list, then the subquery must
provide values for every column in the table.

See Also:

"[Inserting Values into Tables:
Examples](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2145074)"

insert_into_clause

Use the `INSERT` `INTO` clause to specify the target object or objects into
which the database is to insert data.

Directory-based sharding uses the same partition extension syntax as system-
based sharding.

DML_table_expression_clause

Use the `INTO` `DML_table_expression_clause` to specify the objects into which
data is being inserted.

schema

Specify the schema containing the table, view, or materialized view. If you
omit `schema`, then the database assumes the object is in your own schema.

table | view | materialized_view | subquery

Specify the name of the table or object table, view or object view,
materialized view, or the column or columns returned by a subquery, into which
rows are to be inserted. If you specify a view or object view, then the
database inserts rows into the base table of the view.

You cannot insert rows into a read-only materialized view. If you insert rows
into a writable materialized view, then the database inserts the rows into the
underlying container table. However, the insertions are overwritten at the
next refresh operation. If you insert rows into an updatable materialized view
that is part of a materialized view group, then the database also inserts the
corresponding rows into the master table.

If any value to be inserted is a `REF` to an object table, and if the object
table has a primary key object identifier, then the column into which you
insert the `REF` must be a `REF` column with a referential integrity or
`SCOPE` constraint to the object table.

If `table`, or the base table of `view`, contains one or more domain index
columns, then this statement executes the appropriate indextype insert
routine.

Issuing an `INSERT` statement against a table fires any `INSERT` triggers
defined on the table.

See Also:

[Oracle Database Data Cartridge Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADDCI4200) for more information on these routines

Restrictions on the DML_table_expression_clause

This clause is subject to the following restrictions:

  * You cannot execute this statement if `table` or the base table of `view` contains any domain indexes marked `IN_PROGRESS` or `FAILED`. 

  * You cannot insert into a partition if any affected index partitions are marked `UNUSABLE`. 

  * With regard to the `ORDER` `BY` clause of the `subquery` in the `DML_table_expression_clause`, ordering is guaranteed only for the rows being inserted, and only within each extent of the table. Ordering of new rows with respect to existing rows is not guaranteed. 

  * If a view was created using the `WITH` `CHECK` `OPTION`, then you can insert into the view only rows that satisfy the defining query of the view. 

  * If a view was created using a single base table, then you can insert rows into the view and then retrieve those values using the `returning_clause`. 

  * You cannot insert rows into a view except with `INSTEAD` `OF` triggers if the defining query of the view contains one of the following constructs: 

    * A set operator
    * A `DISTINCT` operator 
    * An aggregate or analytic function
    * A `GROUP` `BY`, `ORDER` `BY`, `MODEL`, `CONNECT` `BY`, or `START` `WITH` clause 
    * A collection expression in a `SELECT` list 
    * A subquery in a `SELECT` list 
    * A subquery designated `WITH READ ONLY`
    * Joins, with some exceptions, as documented in [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN020)
    *   * If you specify an index, index partition, or index subpartition that has been marked `UNUSABLE`, then the `INSERT` statement will fail unless the `SKIP_UNUSABLE_INDEXES` session parameter has been set to `TRUE`. Refer to [ALTER SESSION](ALTER-SESSION.md#GUID-27186B28-7EFC-4998-B1ED-2B905CC0211B) for information on the `SKIP_UNUSABLE_INDEXES` session parameter. 

partition_extension_clause

Specify the name or partition key value of the partition or subpartition
within `table`, or the base table of `view`, targeted for inserts.

If a row to be inserted does not map into a specified partition or
subpartition, then the database returns an error.

Restriction on Target Partitions and Subpartitions

This clause is not valid for object tables or object views.

See Also:

"[References to Partitioned Tables and Indexes](Syntax-for-Schema-Objects-and-
Parts-in-SQL-Statements.md#GUID-FED2E424-3F06-4B2B-88D2-DE043CA6E0E4)"

dblink

Specify a complete or partial name of a database link to a remote database
where the table or view is located. You can insert rows into a remote table or
view only if you are using Oracle Database distributed functionality.

If you omit `dblink`, then Oracle Database assumes that the table or view is
on the local database.

Note:

Starting with Oracle Database 12c Release 2 (12.2), the `INSERT` statement
accepts remote LOB locators as bind variables. Refer to the âDistributed
LOBsâ chapter in [Oracle Database SecureFiles and Large Objects Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADLOB-GUID-7E450E86-3E4E-4714-A164-FD36B93722F6) for more
information.

See Also:

  * "[Syntax for Schema Objects and Parts in SQL Statements](Syntax-for-Schema-Objects-and-Parts-in-SQL-Statements.md#GUID-1164C6E0-ABAB-49C2-8821-6B6C5047FEDD)" and "[References to Objects in Remote Databases](Syntax-for-Schema-Objects-and-Parts-in-SQL-Statements.md#GUID-61D0B206-A5EA-473F-AD04-7067D6E3914C)" for information on referring to database links 

  * "[Inserting into a Remote Database: Example](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2126166)"

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

See Also:

"[Table Collections: Examples](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2071643)"

t_alias

Specify a correlation name, which is an alias for the table, view,
materialized view, or subquery to be referenced elsewhere in the statement.

Restriction on Table Aliases

You cannot specify `t_alias` during a multi-table insert.

column

Specify a column of the table, view, or materialized view. In the inserted
row, each column in this list is assigned a value from the
`insert_values_clause` or the subquery. If you want to assign a value to an
`INVISIBLE` column, then you must include the column in this list.

If you omit one or more of the table's columns from this list, then the column
value of that column for the inserted row is the column default value as
specified when the table was created or last altered. If any omitted column
has a `NOT` `NULL` constraint and no default value, then the database returns
an error indicating that the constraint has been violated and rolls back the
`INSERT` statement. Refer to [CREATE TABLE](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6) for more information on
default column values.

If you omit the column list altogether, then the `insert_values_clause` or
query must specify values for all columns in the table.

insert_values_clause

For a single-table insert operation, specify a row of values to be inserted
into the table or view. You must specify a value in the `insert_values_clause`
for each column in the column list. If you omit the column list, then the
`insert_values_clause` must provide values for every column in the table.

You can only supply one set of values for each `insert_into_clause` in a
multi-table insert operation.

In a multi-table insert operation, each expression in the
`insert_values_clause` must refer to columns returned by the select list of
the subquery. If you omit the `insert_values_clause`, then the select list of
the subquery determines the values to be inserted, so it must have the same
number of columns as the column list of the corresponding
`insert_into_clause`. If you do not specify a column list in the
`insert_into_clause`, then the computed row must provide values for all
columns in the target table.

For both types of insert operations, if you specify a column list in the
`insert_into_clause`, then the database assigns to each column in the list a
corresponding value from the values clause or the subquery. You can specify
`DEFAULT` for any value in the `insert_values_clause`. If you have specified a
default value for the corresponding column of the table or view, then that
value is inserted. If no default value for the corresponding column has been
specified, then the database inserts null. Refer to "[About SQL
Expressions](About-SQL-
Expressions.md#GUID-68789A5C-B142-496F-ADEE-837F75F95B2B)" and
[SELECT](SELECT.md#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6) for syntax of
valid expressions.

Restrictions on Inserted Values

Values are subject to the following restrictions:

  * You cannot insert a `BFILE` value until you have initialized the `BFILE` locator to null or to a directory name and filename. 

  * When inserting into a list-partitioned table, you cannot insert a value into the partitioning key column that does not already exist in the `partition_key_value` list of one of the partitions. 

  * You cannot specify `DEFAULT` when inserting into a view. 

  * If you insert string literals into a `RAW` column, then during subsequent queries Oracle Database will perform a full table scan rather than using any index that might exist on the `RAW` column. 

  * Default values for columns are disallowed in row value expressions.

See Also:

  * [BFILENAME](BFILENAME.md#GUID-1F767077-7C26-4962-9833-1433F1749621) for information on initializing `BFILE` values and for an example of inserting into a `BFILE`

  * [Oracle Database SecureFiles and Large Objects Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADLOB002) for information on initializing `BFILE` locators 

  * "[Using XML in SQL Statements](Using-XML-in-SQL-Statements.md#GUID-5FE21EC9-1F66-45F1-9FD8-ECA5336EDC14)" for information on inserting values into an XMLType table 

  * "[Inserting into a Substitutable Tables and Columns: Examples](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2085891)", "[Inserting Using the TO_LOB Function: Example](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2085882)", "[Inserting Sequence Values: Example](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2102477)", and "[Inserting Using Bind Variables: Example](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2126188)"

returning_clause

The returning clause retrieves the rows affected by a DML statement. You can
specify this clause for tables and materialized views and for views with a
single base table.

When operating on a single row, a DML statement with a `returning_clause` can
retrieve column expressions using the affected row, rowid, and `REFs` to the
affected row and store them in host variables or PL/SQL variables.

When operating on multiple rows, a DML statement with the `returning_clause`
stores values from expressions, rowids, and `REFs` involving the affected rows
in bind arrays.

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

Restrictions

The following restrictions apply to the `RETURNING` clause:

  * The `expr` is restricted as follows: 

    * For `UPDATE` and `DELETE` statements each `expr` must be a simple expression or a single-set aggregate function expression. You cannot combine simple expressions and single-set aggregate function expressions in the same `returning_clause`. For `INSERT` statements, each `expr` must be a simple expression. Aggregate functions are not supported in an `INSERT` statement `RETURNING` clause. 

    * Single-set aggregate function expressions cannot include the `DISTINCT` keyword. 

  * If the `expr` list contains a primary key column or other `NOT` `NULL` column, then the update statement fails if the table has a `BEFORE` `UPDATE` trigger defined on it. 

  * You cannot specify the `returning_clause` for a multi-table insert. 

  * You cannot use this clause with parallel DML or with remote objects.

  * You cannot retrieve `LONG` types with this clause. 

  * You cannot specify this clause for a view on which an `INSTEAD` `OF` trigger has been defined. 

See Also:

[Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS005) for information on using the `BULK` `COLLECT`
clause to return multiple values to collection variables

multi_table_insert

In a multi-table insert, you insert rows returned from the evaluation of a
subquery into one or more tables.

Table aliases are not defined by the select list of the subquery. Therefore,
they are not visible in the clauses dependent on the select list. For example,
this can happen when trying to refer to an object column in an expression. To
use an expression with a table alias, you must put the expression into the
select list with a column alias, and then refer to the column alias in the
`VALUES` clause or `WHEN` condition of the multi-table insert.

ALL into_clause

Specify `ALL` followed by multiple `insert_into_clauses` to perform an
unconditional multi-table insert. Oracle Database executes each
`insert_into_clause` once for each row returned by the subquery.

Restrictions Using INSERT ALL

  * The maximum number of rows you can insert into a table with 4096 columns is 15. 

  * The maximum number of rows you can insert into a table with 1000 columns is 65.

  * The maximum row limit for tables with fewer columns is not constant and may vary.

conditional_insert_clause

Specify the `conditional_insert_clause` to perform a conditional multi-table
insert.

You can only supply one set of values for each `WHEN` or `ELSE` clause of
`conditional_insert_clause`.

Oracle Database filters each `insert_into_clause` through the corresponding
`WHEN` condition, which determines whether that `insert_into_clause` is
executed. Each expression in the `WHEN` condition must refer to columns
returned by the select list of the subquery.A single multi-table insert
statement can contain up to 127 `WHEN` clauses.

ALL

If you specify `ALL`, the default value, then the database evaluates each
`WHEN` clause regardless of the results of the evaluation of any other `WHEN`
clause. For each `WHEN` clause whose condition evaluates to true, the database
executes the corresponding `INTO` clause list.

FIRST

If you specify `FIRST`, then the database evaluates each `WHEN` clause in the
order in which it appears in the statement. For the first `WHEN` clause that
evaluates to true, the database executes the corresponding `INTO` clause and
skips subsequent `WHEN` clauses for the given row.

ELSE clause

For a given row, if no `WHEN` clause evaluates to true, then:

  * If you have specified an `ELSE` clause, then the database executes the `INTO` clause list associated with the `ELSE` clause. 

  * If you did not specify an else clause, then the database takes no action for that row.

See Also:

"[Multi-Table Inserts:
Examples](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2125362)"

Restrictions on Multi-Table Inserts

multi-table inserts are subject to the following restrictions:

  * You can perform multi-table inserts only on tables, not on views or materialized views.

  * You cannot perform a multi-table insert into a remote table.

  * You cannot specify a `TABLE` collection expression when performing a multi-table insert. 

  * multi-table inserts are not parallelized if any target table is index organized or if any target table has a bitmap index defined on it.

  * Plan stability is not supported for multi-table insert statements.

  * The subquery of the multitable insert statement cannot use a sequence. For rules pertaining to sequences, see [How to Use Sequence Values](Sequence-Pseudocolumns.md#GUID-55228D7B-9CF1-4496-8524-3CD1DD4773FD)

subquery

Specify a subquery that returns rows that are inserted into the table. The
subquery can refer to any table, view, or materialized view, including the
target tables of the `INSERT` statement. If the subquery selects no rows, then
the database inserts no rows into the table.

You can use `subquery` in combination with the `TO_LOB` function to convert
the values in a `LONG` column to LOB values in another column in the same or
another table.

  * To migrate `LONG` values to LOB values in another column in a view, you must perform the migration on the base table and then add the LOB column to the view. 

  * To migrate `LONG` values on a remote table to LOB values in a local table, you must perform the migration on the remote table using the `TO_LOB` function, and then perform an `INSERT` ... `subquery` operation to copy the LOB values from the remote table into the local table. 

Notes on Inserting with a Subquery

The following notes apply when inserting with a subquery:

  * If `subquery` returns the partial or total equivalent of a materialized view, then the database may use the materialized view for query rewrite in place of one or more tables specified in `subquery`. 

See Also:

Oracle Database Data Warehousing Guide for more information on [materialized
views](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DWHSG008) and [query
rewrite](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DWHSG018)

  * If `subquery` refers to remote objects, then the `INSERT` operation can run in parallel as long as the reference does not loop back to an object on the local database. However, if the `subquery` in the `DML_table_expression_clause` refers to any remote objects, then the `INSERT` operation will run serially without notification. See [parallel_clause](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2159323) for more information. 

  * If `subquery` includes an `ORDER` `BY` clause, then it will override row ordering specified using attribute clustering table properties. 

See Also:

  * "[Inserting Values with a Subquery: Example](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__I2126076)"

  * [BFILENAME](BFILENAME.md#GUID-1F767077-7C26-4962-9833-1433F1749621) for an example of inserting into a `BFILE`

  * [Oracle Database SecureFiles and Large Objects Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADLOB012) for information on initializing `BFILE`s 

  * "[About SQL Expressions](About-SQL-Expressions.md#GUID-68789A5C-B142-496F-ADEE-837F75F95B2B)" and [SELECT](SELECT.md#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6) for syntax of valid expressions 

error_logging_clause

The `error_logging_clause` lets you capture DML errors and the log column
values of the affected rows and save them in an error logging table.

INTO table

Specify the name of the error logging table. If you omit this clause, then the
database assigns the default name generated by the `DBMS_ERRLOG` package. The
default error log table name is `ERR$_` followed by the first 25 characters of
the name of the table upon which the DML operation is being executed.

simple_expression

Specify the value to be used as a statement tag, so that you can identify the
errors from this statement in the error logging table. The expression can be
either a text literal, a number literal, or a general SQL expression such as a
bind variable. You can also use a function expression if you convert it to a
text literal â for example, `TO_CHAR(SYSDATE)`.

REJECT LIMIT

This clause lets you specify an integer as an upper limit for the number of
errors to be logged before the statement terminates and rolls back any changes
made by the statement. The default rejection limit is zero. For parallel DML
operations, the reject limit is applied to each parallel server.

Restrictions on DML Error Logging

  * The following conditions cause the statement to fail and roll back without invoking the error logging capability:

    * Violated deferred constraints.

    * Any direct-path `INSERT` or `MERGE` operation that raises a unique constraint or index violation. 

    * Any update operation `UPDATE` or `MERGE` that raises a unique constraint or index violation. 

  * You cannot track errors in the error logging table for `LONG`, LOB, or object type columns. However, the table that is the target of the DML operation can contain these types of columns. 

    * If you create or modify the corresponding error logging table so that it contains a column of an unsupported type, and if the name of that column corresponds to an unsupported column in the target DML table, then the DML statement fails at parse time.

    * If the error logging table does not contain any unsupported column types, then all DML errors are logged until the reject limit of errors is reached. For rows on which errors occur, column values with corresponding columns in the error logging table are logged along with the control information.

See Also:

  * [Oracle Database PL/SQL Packages and Types Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS680) for information on using the `create_error_log` procedure of the `DBMS_ERRLOG` package and [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN10261) for general information on DML error logging. 

  * "[Inserting Into a Table with Error Logging: Example](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__BCEGDJDJ)"

Examples

Inserting Values into Tables: Examples

The following statement inserts a row into the sample table `departments`:

    
    
    INSERT INTO departments
       VALUES (280, 'Recreation', 121, 1700);
    

If the `departments` table had been created with a default value of 121 for
the `manager_id` column, then you could issue the same statement as follows:

    
    
    INSERT INTO departments
       VALUES (280, 'Recreation', DEFAULT, 1700);
    

The following statement inserts a row with six columns into the `employees`
table. One of these columns is assigned `NULL` and another is assigned a
number in scientific notation:

    
    
    INSERT INTO employees (employee_id, last_name, email, 
          hire_date, job_id, salary, commission_pct) 
       VALUES (207, 'Gregory', 'pgregory@example.com', 
          sysdate, 'PU_CLERK', 1.2E3, NULL);
    

The following statement has the same effect as the preceding example, but uses
a subquery in the `DML_table_expression_clause`:

    
    
    INSERT INTO 
       (SELECT employee_id, last_name, email, hire_date, job_id, 
          salary, commission_pct FROM employees) 
       VALUES (207, 'Gregory', 'pgregory@example.com', 
          sysdate, 'PU_CLERK', 1.2E3, NULL);

Inserting Values with a Subquery: Example

The following statement copies employees whose commission exceeds 25% of their
salary into the `bonuses` table, which was created in "[Merging into a Table:
Example](MERGE.md#GUID-5692CCB7-24D9-4C0E-81A7-A22436DC968F__I2091840)":

    
    
    INSERT INTO bonuses
       SELECT employee_id, salary*1.1 
       FROM employees
       WHERE commission_pct > 0.25; 

Inserting Into a Table with Error Logging: Example

The following statements create a `raises` table in the sample schema `hr`,
create an error logging table using the `DBMS_ERRLOG` package, and populate
the `raises` table with data from the `employees` table. One of the inserts
violates the check constraint on `raises`, and that row can be seen in
`errlog`. If more than ten errors had occurred, then the statement would have
aborted, rolling back any insertions made:

    
    
    CREATE TABLE raises (emp_id NUMBER, sal NUMBER 
       CONSTRAINT check_sal CHECK(sal > 8000));
    
    EXECUTE DBMS_ERRLOG.CREATE_ERROR_LOG('raises', 'errlog');
    
    
    
    INSERT INTO raises
       SELECT employee_id, salary*1.1 FROM employees
       WHERE commission_pct > .2
       LOG ERRORS INTO errlog ('my_bad') REJECT LIMIT 10;
    
    SELECT ORA_ERR_MESG$, ORA_ERR_TAG$, emp_id, sal FROM errlog;
    
    ORA_ERR_MESG$               ORA_ERR_TAG$         EMP_ID SAL
    --------------------------- -------------------- ------ -------
    ORA-02290: check constraint my_bad               161    7700
     (HR.SYS_C004266) violated

Inserting into a Remote Database: Example

The following statement inserts a row into the `employees` table owned by the
user `hr` on the database accessible by the database link `remote`:

    
    
    INSERT INTO employees@remote
       VALUES (8002, 'Juan', 'Fernandez', 'juanf@example.com', NULL, 
       TO_DATE('04-OCT-1992', 'DD-MON-YYYY'), 'SH_CLERK', 3000, 
       NULL, 121, 20); 

Inserting Sequence Values: Example

The following statement inserts a new row containing the next value of the
`departments_seq` sequence into the `departments` table:

    
    
    INSERT INTO departments 
       VALUES  (departments_seq.nextval, 'Entertainment', 162, 1400); 

Inserting Using Bind Variables: Example

The following example returns the values of the inserted rows into output bind
variables :`bnd1` and :`bnd2`. The bind variables must first be declared.

    
    
    INSERT INTO employees 
          (employee_id, last_name, email, hire_date, job_id, salary)
       VALUES 
       (employees_seq.nextval, 'Doe', 'john.doe@example.com', 
           SYSDATE, 'SH_CLERK', 2400) 
       RETURNING salary*12, job_id INTO :bnd1, :bnd2;

Inserting into a Substitutable Tables and Columns: Examples

The following example inserts into the `persons` table, which is created in
"[Substitutable Table and Column Examples](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2090577)". The first
statement uses the root type `person_t`. The second insert uses the
`employee_t` subtype of `person_t`, and the third insert uses the
`part_time_emp_t` subtype of `employee_t`:

    
    
    INSERT INTO persons VALUES (person_t('Bob', 1234));
    INSERT INTO persons VALUES (employee_t('Joe', 32456, 12, 100000));
    INSERT INTO persons VALUES (
       part_time_emp_t('Tim', 5678, 13, 1000, 20));
    

The following example inserts into the `books` table, which was created in
"[Substitutable Table and Column Examples](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2090577)". Notice that
specification of the attribute values is identical to that for the
substitutable table example:

    
    
    INSERT INTO books VALUES (
       'An Autobiography', person_t('Bob', 1234));
    INSERT INTO books VALUES (
       'Business Rules', employee_t('Joe', 3456, 12, 10000));
    INSERT INTO books VALUES (
       'Mixing School and Work', 
       part_time_emp_t('Tim', 5678, 13, 1000, 20));
    

You can extract data from substitutable tables and columns using built-in
functions and conditions. For examples, see the functions
[TREAT](TREAT.md#GUID-037C0CD3-C256-4A02-80E0-C6F15147C5BF) and
[SYS_TYPEID](SYS_TYPEID.md#GUID-4E3D45A1-7433-495D-9062-88505A1496E0), and
"[IS OF type Condition](IS-OF-type-
Condition.md#GUID-7254E4C7-0194-4C1F-A3B2-2CFB0AD907CD)".

Inserting Using the TO_LOB Function: Example

The following example copies `LONG` data to a LOB column in the following
`long_tab` table:

    
    
    CREATE TABLE long_tab (pic_id NUMBER, long_pics LONG RAW);
    

First you must create a table with a LOB.

    
    
    CREATE TABLE lob_tab (pic_id NUMBER, lob_pics BLOB);
    

Next, use an `INSERT` ... `SELECT` statement to copy the data in all rows for
the `LONG` column into the newly created LOB column:

    
    
    INSERT INTO lob_tab 
       SELECT pic_id, TO_LOB(long_pics) FROM long_tab;
    

When you are confident that the migration has been successful, you can drop
the `long_pics` table. Alternatively, if the table contains other columns,
then you can simply drop the `LONG` column from the table as follows:

    
    
    ALTER TABLE long_tab DROP COLUMN long_pics;

Multi-Table Inserts: Examples

The following example uses the multi-table insert syntax to insert into the
sample table `sh.sales` some data from an input table with a different
structure.

Note:

A number of `NOT` `NULL` constraints on the `sales` table have been disabled
for purposes of this example, because the example ignores a number of table
columns for the sake of brevity.

The input table looks like this:

    
    
    SELECT * FROM sales_input_table;
    
    
    
    PRODUCT_ID CUSTOMER_ID WEEKLY_ST  SALES_SUN  SALES_MON  SALES_TUE  SALES_WED SALES_THU  SALES_FRI  SALES_SAT
    ---------- ----------- --------- ---------- ---------- ---------- -------------------- ---------- ----------
           111         222 01-OCT-00        100        200        300        400       500        600        700
           222         333 08-OCT-00        200        300        400        500       600        700        800
           333         444 15-OCT-00        300        400        500        600       700        800        900

The multi-table insert statement looks like this:

    
    
    INSERT ALL
          INTO sales (prod_id, cust_id, time_id, amount)
          VALUES (product_id, customer_id, weekly_start_date, sales_sun)
          INTO sales (prod_id, cust_id, time_id, amount)
          VALUES (product_id, customer_id, weekly_start_date+1, sales_mon)
          INTO sales (prod_id, cust_id, time_id, amount)
          VALUES (product_id, customer_id, weekly_start_date+2, sales_tue)
          INTO sales (prod_id, cust_id, time_id, amount)
          VALUES (product_id, customer_id, weekly_start_date+3, sales_wed)
          INTO sales (prod_id, cust_id, time_id, amount)
          VALUES (product_id, customer_id, weekly_start_date+4, sales_thu)
          INTO sales (prod_id, cust_id, time_id, amount)
          VALUES (product_id, customer_id, weekly_start_date+5, sales_fri)
          INTO sales (prod_id, cust_id, time_id, amount)
          VALUES (product_id, customer_id, weekly_start_date+6, sales_sat)
       SELECT product_id, customer_id, weekly_start_date, sales_sun,
          sales_mon, sales_tue, sales_wed, sales_thu, sales_fri, sales_sat
          FROM sales_input_table;
    

Assuming these are the only rows in the `sales` table, the contents now look
like this:

    
    
    SELECT * FROM sales
       ORDER BY prod_id, cust_id, time_id;
    
       PROD_ID    CUST_ID TIME_ID   C   PROMO_ID QUANTITY_SOLD     AMOUNT       COST
    ---------- ---------- --------- - ---------- ------------- ---------- ----------
           111        222 01-OCT-00                                   100
           111        222 02-OCT-00                                   200
           111        222 03-OCT-00                                   300
           111        222 04-OCT-00                                   400
           111        222 05-OCT-00                                   500
           111        222 06-OCT-00                                   600
           111        222 07-OCT-00                                   700
           222        333 08-OCT-00                                   200
           222        333 09-OCT-00                                   300
           222        333 10-OCT-00                                   400
           222        333 11-OCT-00                                   500
           222        333 12-OCT-00                                   600
           222        333 13-OCT-00                                   700
           222        333 14-OCT-00                                   800
           333        444 15-OCT-00                                   300
           333        444 16-OCT-00                                   400
           333        444 17-OCT-00                                   500
           333        444 18-OCT-00                                   600
           333        444 19-OCT-00                                   700
           333        444 20-OCT-00                                   800
           333        444 21-OCT-00                                   900
    

The next examples insert into multiple tables. Suppose you want to provide to
sales representatives some information on orders of various sizes. The
following example creates tables for small, medium, large, and special orders
and populates those tables with data from the sample table `oe.orders`:

    
    
    CREATE TABLE small_orders 
       (order_id       NUMBER(12)   NOT NULL,
        customer_id    NUMBER(6)    NOT NULL,
        order_total    NUMBER(8,2),
        sales_rep_id   NUMBER(6)
       );
    
    CREATE TABLE medium_orders AS SELECT * FROM small_orders;
    
    CREATE TABLE large_orders AS SELECT * FROM small_orders;
    
    CREATE TABLE special_orders 
       (order_id       NUMBER(12)    NOT NULL,
        customer_id    NUMBER(6)     NOT NULL,
        order_total    NUMBER(8,2),
        sales_rep_id   NUMBER(6),
        credit_limit   NUMBER(9,2),
        cust_email     VARCHAR2(40)
       );
    

The first multi-table insert populates only the tables for small, medium, and
large orders:

    
    
    INSERT ALL
       WHEN order_total <= 100000 THEN
          INTO small_orders
       WHEN order_total > 1000000 AND order_total <= 200000 THEN
          INTO medium_orders
       WHEN order_total > 200000 THEN
          INTO large_orders
       SELECT order_id, order_total, sales_rep_id, customer_id
          FROM orders;
    

You can accomplish the same thing using the `ELSE` clause in place of the
insert into the `large_orders` table:

    
    
    INSERT ALL
       WHEN order_total <= 100000 THEN
          INTO small_orders
       WHEN order_total > 100000 AND order_total <= 200000 THEN
          INTO medium_orders
       ELSE
          INTO large_orders
       SELECT order_id, order_total, sales_rep_id, customer_id
          FROM orders;
    

The next example inserts into the small, medium, and large tables, as in the
preceding example, and also puts orders greater than 290,000 into the
`special_orders` table. This table also shows how to use column aliases to
simplify the statement:

    
    
    INSERT ALL
       WHEN ottl <= 100000 THEN
          INTO small_orders
             VALUES(oid, ottl, sid, cid)
       WHEN ottl > 100000 and ottl <= 200000 THEN
          INTO medium_orders 
             VALUES(oid, ottl, sid, cid)
       WHEN ottl > 200000 THEN
          into large_orders
             VALUES(oid, ottl, sid, cid)
       WHEN ottl > 290000 THEN
          INTO special_orders
       SELECT o.order_id oid, o.customer_id cid, o.order_total ottl,
          o.sales_rep_id sid, c.credit_limit cl, c.cust_email cem
          FROM orders o, customers c
          WHERE o.customer_id = c.customer_id;
    

Finally, the next example uses the `FIRST` clause to put orders greater than
290,000 into the `special_orders` table and exclude those orders from the
`large_orders` table:

    
    
    INSERT FIRST
       WHEN ottl <= 100000 THEN
          INTO small_orders
             VALUES(oid, ottl, sid, cid)
       WHEN ottl > 100000 and ottl <= 200000 THEN
          INTO medium_orders
             VALUES(oid, ottl, sid, cid)
       WHEN ottl > 290000 THEN
          INTO special_orders
       WHEN ottl > 200000 THEN
          INTO large_orders
             VALUES(oid, ottl, sid, cid)
       SELECT o.order_id oid, o.customer_id cid, o.order_total ottl,
          o.sales_rep_id sid, c.credit_limit cl, c.cust_email cem
          FROM orders o, customers c
          WHERE o.customer_id = c.customer_id;

Inserting Multiple Rows Using a Single Statement: Example

The following statements create three tables named people, patients and staff:

    
    
    CREATE TABLE people ( 
      person_id   INTEGER NOT NULL PRIMARY KEY, 
      given_name  VARCHAR2(100) NOT NULL, 
      family_name VARCHAR2(100) NOT NULL, 
      title       VARCHAR2(20), 
      birth_date  DATE 
    );
    
    CREATE TABLE patients ( 
      patient_id          INTEGER NOT NULL PRIMARY KEY REFERENCES people (person_id), 
      last_admission_date DATE 
    );
    
    CREATE TABLE staff ( 
      staff_id   INTEGER NOT NULL PRIMARY KEY REFERENCES people (person_id), 
      hired_date DATE 
    );

The following statement inserts a row into the people table:

    
    
    INSERT INTO people 
    VALUES (1, 'Dave', 'Badger', 'Mr', date'1960-05-01');

The following statement returns an error as there is no value provided for the
birth_date column:

    
    
    INSERT INTO people 
    VALUES (2, 'Simon', 'Fox', 'Mr');

The following statement inserts a row into the people table:

    
    
    INSERT INTO people (person_id, given_name, family_name, title) 
    VALUES (2, 'Simon', 'Fox', 'Mr');

The following statement inserts a row into the people table and the value for
the title column is populated by selecting a static value from the dual table:

    
    
    INSERT INTO people (person_id, given_name, family_name, title) 
    VALUES (3, 'Dave', 'Frog', (SELECT 'Mr' FROM dual));

The following statement inserts multiple rows into the people table using
âSELECTâ statement:

    
    
    INSERT INTO people (person_id, given_name, family_name, title) 
      WITH names AS ( 
        SELECT 4, 'Ruth',     'Fox',      'Mrs'    FROM dual UNION ALL 
        SELECT 5, 'Isabelle', 'Squirrel', 'Miss'   FROM dual UNION ALL 
        SELECT 6, 'Justin',   'Frog',     'Master' FROM dual UNION ALL 
        SELECT 7, 'Lisa',     'Owl',      'Dr'     FROM dual 
      ) 
      SELECT * FROM names;

The following statement rolls back all the previous DML operations:

    
    
    ROLLBACK;

The following statement inserts multiple rows into the people table using
âSELECTâ statement with a âWHEREâ condition:

    
    
    INSERT INTO people (person_id, given_name, family_name, title) 
      WITH names AS ( 
        SELECT 4, 'Ruth',     'Fox' family_name,      'Mrs'    FROM dual UNION ALL 
        SELECT 5, 'Isabelle', 'Squirrel' family_name, 'Miss'   FROM dual UNION ALL 
        SELECT 6, 'Justin',   'Frog' family_name,     'Master' FROM dual UNION ALL 
        SELECT 7, 'Lisa',     'Owl' family_name,      'Dr'     FROM dual 
      ) 
      SELECT * FROM names 
      WHERE  family_name LIKE 'F%';

The following statement rolls back all the previous DML operations:

    
    
    ROLLBACK;

The following statement inserts multiple rows into people, patients and staff
table using âINSERT ALLâ statement:

    
    
    INSERT ALL 
      /* Every one is a person */ 
      INTO people (person_id, given_name, family_name, title) 
        VALUES (id, given_name, family_name, title) 
      INTO patients (patient_id, last_admission_date) 
        VALUES (id, admission_date) 
      INTO staff (staff_id, hired_date) 
        VALUES (id, hired_date) 
      WITH names AS ( 
        SELECT 4 id, 'Ruth' given_name, 'Fox' family_name, 'Mrs' title, 
               NULL hired_date, DATE'2009-12-31' admission_date 
        FROM   dual UNION ALL 
        SELECT 5 id, 'Isabelle' given_name, 'Squirrel' family_name, 'Miss' title , 
               NULL hired_date, DATE'2014-01-01' admission_date 
        FROM   dual UNION ALL 
        SELECT 6 id, 'Justin' given_name, 'Frog' family_name, 'Master' title, 
               NULL hired_date, DATE'2015-04-22' admission_date 
        FROM   dual UNION ALL 
        SELECT 7 id, 'Lisa' given_name, 'Owl' family_name, 'Dr' title, 
               DATE'2015-01-01' hired_date, NULL admission_date 
        FROM   dual 
      ) 
      SELECT * FROM names;

The following statement rolls back all the previous DML operations:

    
    
    ROLLBACK;

The following statement inserts multiple rows into people, patients and staff
table using âINSERT ALLâ statement with various conditions:

    
    
    INSERT ALL 
      /* Everyone is a person, so insert all rows into people */ 
      WHEN 1=1 THEN 
        INTO people (person_id, given_name, family_name, title) 
        VALUES (id, given_name, family_name, title) 
      /* Only people with an admission date are patients */ 
      WHEN admission_date IS NOT NULL THEN 
        INTO patients (patient_id, last_admission_date) 
        VALUES (id, admission_date) 
      /* Only people with a hired date are staff */ 
      WHEN hired_date IS NOT NULL THEN 
        INTO staff (staff_id, hired_date) 
        VALUES (id, hired_date) 
      WITH names AS ( 
        SELECT 4 id, 'Ruth' given_name, 'Fox' family_name, 'Mrs' title, 
               NULL hired_date, DATE'2009-12-31' admission_date 
        FROM   dual UNION ALL 
        SELECT 5 id, 'Isabelle' given_name, 'Squirrel' family_name, 'Miss' title , 
               NULL hired_date, DATE'2014-01-01' admission_date 
        FROM   dual UNION ALL 
        SELECT 6 id, 'Justin' given_name, 'Frog' family_name, 'Master' title, 
               NULL hired_date, DATE'2015-04-22' admission_date 
        FROM   dual UNION ALL 
        SELECT 7 id, 'Lisa' given_name, 'Owl' family_name, 'Dr' title, 
               DATE'2015-01-01' hired_date, NULL admission_date 
        FROM   dual 
      ) 
      SELECT * FROM names;


[← Previous](GRANT.md)

[Next →](LOCK-TABLE.md)
