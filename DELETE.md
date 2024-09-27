[Previous](CREATE-VIEW.md) [Next](DISASSOCIATE-STATISTICS.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: CREATE SEQUENCE to DROP CLUSTER](SQL-Statements-CREATE-SEQUENCE-to-DROP-CLUSTER.md)
  3. DELETE 

## DELETE

Purpose

Use the `DELETE` statement to remove rows from:

  * An unpartitioned or partitioned table

  * The unpartitioned or partitioned base table of a view

  * The unpartitioned or partitioned container table of a writable materialized view

  * The unpartitioned or partitioned master table of an updatable materialized view

Prerequisites

For you to delete rows from a table, the table must be in your own schema or
you must have the `DELETE` object privilege on the table.

For you to delete rows from an updatable materialized view, the materialized
view must be in your own schema or you must have the `DELETE` object privilege
on the materialized view.

For you to delete rows from the base table of a view, the owner of the schema
containing the view must have the `DELETE` object privilege on the base table.
Also, if the view is in a schema other than your own, then you must have the
`DELETE` object privilege on the view.

The `DELETE` `ANY` `TABLE` system privilege also allows you to delete rows
from any table or table partition or from the base table of any view.

To delete rows from an object on a remote database, you must also have the
`READ` or `SELECT` object privilege on the object.

If the `SQL92_SECURITY` initialization parameter is set to `TRUE` and the
`DELETE` operation references table columns, such as the columns in a
`where_clause`, then you must also have the `SELECT` object privilege on the
object from which you want to delete rows.

You cannot delete rows from a table if a function-based index on the table has
become invalid. You must first validate the function-based index.

Syntax

delete::=

![Description of delete.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/delete.gif)  
[Description of the illustration delete.eps](img_text/delete.md)

([DML_table_expression_clause::=](DELETE.md#GUID-156845A5-B626-412B-9F95-8869B988ABD7__I2122534),
[where_clause::=](DELETE.md#GUID-156845A5-B626-412B-9F95-8869B988ABD7__I2122549),
[returning_clause::=](DELETE.md#GUID-156845A5-B626-412B-9F95-8869B988ABD7__I2122564),
[error_logging_clause::=](DELETE.md#GUID-156845A5-B626-412B-9F95-8869B988ABD7__CEGCHDJF),
[from_using_clause::=](DELETE.md#GUID-156845A5-B626-412B-9F95-8869B988ABD7__SECTION_QS3_4WS_DYB))

DML_table_expression_clause::=

![Description of dml_table_expression_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/dml_table_expression_clause.gif)  
[Description of the illustration
dml_table_expression_clause.eps](img_text/dml_table_expression_clause.md)

([partition_extension_clause::=](DELETE.md#GUID-156845A5-B626-412B-9F95-8869B988ABD7__BABEAAJA),
[subquery::=](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2126435),
[subquery_restriction_clause::=](DELETE.md#GUID-156845A5-B626-412B-9F95-8869B988ABD7__I2122580),
[table_collection_expression::=](DELETE.md#GUID-156845A5-B626-412B-9F95-8869B988ABD7__I2122595))

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

from_using_clause::=

  

![Description of from_using_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/from_using_clause.gif)  
[Description of the illustration
from_using_clause.eps](img_text/from_using_clause.md)

  

where_clause::=

![Description of where_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/where_clause.gif)  
[Description of the illustration where_clause.eps](img_text/where_clause.md)

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

See Also:

"[Hints](Comments.md#GUID-D316D545-89E2-4D54-977F-FC97815CD62E)" for the
syntax and description of hints

from_clause

Use the `FROM` clause to specify the database objects from which you are
deleting rows.

The `ONLY` syntax is relevant only for views. Use the `ONLY` clause if the
view in the `FROM` clause belongs to a view hierarchy and you do not want to
delete rows from any of its subviews.

DML_table_expression_clause

Use this clause to specify the objects from which data is being deleted.

schema

Specify the schema containing the table or view. If you omit `schema`, then
Oracle Database assumes the table or view is in your own schema.

table | view | materialized view | subquery

Specify the name of a table, view, materialized view, or the column or columns
resulting from a subquery, from which the rows are to be deleted.

When you delete rows from an updatable view, Oracle Database deletes rows from
the base table.

You cannot delete rows from a read-only materialized view. If you delete rows
from a writable materialized view, then the database removes the rows from the
underlying container table. However, the deletions are overwritten at the next
refresh operation. If you delete rows from an updatable materialized view that
is part of a materialized view group, then the database also removes the
corresponding rows from the master table.

If `table` or the base table of `view` or the master table of
`materialized_view` contains one or more domain index columns, then this
statement executes the appropriate indextype delete routine.

See Also:

[Oracle Database Data Cartridge Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADDCI4210) for more information on these routines

Issuing a `DELETE` statement against a table fires any `DELETE` triggers
defined on the table.

All table or index space released by the deleted rows is retained by the table
and index.

partition_extension_clause

Specify the name or partition key value of the partition or subpartition
targeted for deletes within the object.

You need not specify the partition name when deleting values from a
partitioned object. However, in some cases, specifying the partition name is
more efficient than a complicated `where_clause`.

See Also:

"[References to Partitioned Tables and Indexes](Syntax-for-Schema-Objects-and-
Parts-in-SQL-Statements.md#GUID-FED2E424-3F06-4B2B-88D2-DE043CA6E0E4)" and
"[Deleting Rows from a Partition:
Example](DELETE.md#GUID-156845A5-B626-412B-9F95-8869B988ABD7__I2126857)"

dblink

Specify the complete or partial name of a database link to a remote database
where the object is located. You can delete rows from a remote object only if
you are using Oracle Database distributed functionality.

Note:

Starting with Oracle Database 12c Release 2 (12.2), the `DELETE` statement
accepts remote LOB locators as bind variables. Refer to the âDistributed
LOBsâ chapter in [Oracle Database SecureFiles and Large Objects Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADLOB-GUID-7E450E86-3E4E-4714-A164-FD36B93722F6) for more
information.

See Also:

"[References to Objects in Remote Databases](Syntax-for-Schema-Objects-and-
Parts-in-SQL-Statements.md#GUID-61D0B206-A5EA-473F-AD04-7067D6E3914C)" for
information on referring to database links and "[Deleting Rows from a Remote
Database:
Example](DELETE.md#GUID-156845A5-B626-412B-9F95-8869B988ABD7__I2126841)"

If you omit `dblink`, then the database assumes that the object is located on
the local database.

subquery_restriction_clause

The `subquery_restriction_clause` lets you restrict the subquery in one of the
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

You can use a `table_collection_expression` in a correlated subquery to delete
rows with values that also exist in another table.

See Also:

"[Table Collections: Examples](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2071643)"

collection_expression

Specify a subquery that selects a nested table column from the object from
which you are deleting.

Restrictions on the dml_table_expression_clause Clause

This clause is subject to the following restrictions:

  * You cannot execute this statement if `table` or the base or master table of `view` or `materialized_view` contains any domain indexes marked `IN_PROGRESS` or `FAILED.`

  * You cannot insert into a partition if any affected index partitions are marked `UNUSABLE`. 

  * You cannot specify the `ORDER` `BY` clause in the subquery of the `DML_table_expression_clause`. 

  * You cannot delete from a view except through `INSTEAD` `OF` triggers if the defining query of the view contains one of the following constructs: 

    * A set operator
    * A `DISTINCT` operator 
    * An aggregate or analytic function
    * A `GROUP` `BY`, `ORDER` `BY`, `MODEL`, `CONNECT` `BY`, or `START` `WITH` clause 
    * A collection expression in a `SELECT` list 
    * A subquery in a `SELECT` list 
    * A subquery designated `WITH READ ONLY`
    * Joins, with some exceptions, as documented in [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN020)

If you specify an index, index partition, or index subpartition that has been
marked `UNUSABLE`, then the `DELETE` statement will fail unless the
`SKIP_UNUSABLE_INDEXES` initialization parameter has been set to `true`.

See Also:

[ALTER SESSION](ALTER-SESSION.md#GUID-27186B28-7EFC-4998-B1ED-2B905CC0211B)

t_alias

Provide a correlation name for the table, view, materialized view, subquery,
or collection value to be referenced elsewhere in the statement. This alias is
required if the `DML_table_expression_clause` references any object type
attributes or object type methods. Table aliases are generally used in
`DELETE` statements with correlated queries.

from_using_clause

Use this clause to filter the rows `DELETE` removes. Specify the join
conditions in the `where_clause`. You can outer join source tables to the
target with (+). The target table cannot be the outer table in the join.

You can join many tables, views, and inline views. Specify the join conditions
in the `where_clause` or use the `join_clause` to join these to each other
with ANSI join syntax.

You can specify the same table in the `dml_table_expression_clause` and
`from_using_clause`. When you do so they must have unique aliases.

Example: Delete with Direct-Join

In this example, the join condition between table `t`and table `s` determines
which rows of `t` are deleted:

    
    
    DELETE FROM t     
    FROM s
    WHERE t.t1 = s.s1;
    

If the join condition results in the same target row being selected more than
once, the `DELETE` will succeed, and the deletion count will correctly reflect
the number of rows deleted.

In a `DELETE` of a join view, one of the tables must be key-preserving. That
table is used as the delete target. If there is more than one table that is
key-preserving, the first key-preserved table encountered in the `FROM` clause
is used as the delete target. If no such table exists, error `ORA-01752` is
raised. There is no such restriction in direct join syntax, since it is clear
what the delete target is.

Direct joins for `DELETE` have the same semantics and restrictions as `SELECT`
in the `from_clause` and `where_clause`. Triggers on the target table fire as
normal.

Restrictions

  * You cannot specify ANSI join syntax using the `dml_table_expression_clause`. However, you can specify ANSI join syntax between the tables specified in the `FROM` clause. Right and full outer joins are not allowed. 

  * You can use a lateral view in the `FROM` clause, but it cannot reference a column from the delete target. It may be outer-joined. 

  * You can only specify one table, view, or materialized view in `dml_table_expression_clause` when the `from_using_clause` is present. 

  * The `hint` clause can be used to specify instructions to the optimizer for joins involving the `from_using_clause`

where_clause

Use the `where_clause` to delete only rows that satisfy the condition. The
condition can reference the object from which you are deleting and can contain
a subquery. You can delete rows from a remote object only if you are using
Oracle Database distributed functionality. Refer to
[Conditions](Conditions.md#GUID-C2E3ED44-16E7-4924-9125-E1693B1022A8) for
the syntax of `condition`.

If this clause contains a `subquery` that refers to remote objects, then the
`DELETE` operation can run in parallel as long as the reference does not loop
back to an object on the local database. However, if the `subquery` in the
`DML_table_expression_clause` refers to any remote objects, then the `DELETE`
operation will run serially without notification. Refer to the
[parallel_clause](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2159323) in the
`CREATE` `TABLE` documentation for additional information.

If you omit `dblink`, then the database assumes that the table or view is
located on the local database.

If you omit the `where_clause`, then the database deletes all rows of the
object.

returning_clause

This clause lets you return values from deleted columns, and thereby eliminate
the need to issue a `SELECT` statement following the `DELETE` statement.

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

Restrictions on the RETURNING Clause

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

  * [Oracle Database PL/SQL Language Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=LNPLS012) for information on using the `BULK` `COLLECT` clause to return multiple values to collection variables 

  * "[Using the RETURNING Clause: Example](DELETE.md#GUID-156845A5-B626-412B-9F95-8869B988ABD7__I2126877)"

error_logging_clause

The `error_logging_clause` has the same behavior in `DELETE` statement as it
does in an `INSERT` statement. Refer to the `INSERT` statement
[error_logging_clause](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__BGBEIACB)
for more information.

See Also:

"[Inserting Into a Table with Error Logging:
Example](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423__BCEGDJDJ)"

Examples

Deleting Rows: Examples

The following statement deletes all rows from the sample table
`oe.product_descriptions` where the value of the `language_id` column is `AR`:

    
    
    DELETE FROM product_descriptions
       WHERE language_id = 'AR';
    

The following statement deletes from the sample table `hr.employees`
purchasing clerks whose commission rate is less than 10%:

    
    
    DELETE FROM employees
       WHERE job_id = 'SA_REP'
       AND commission_pct < .2;
    

The following statement has the same effect as the preceding example, but uses
a subquery:

    
    
    DELETE FROM (SELECT * FROM employees)
       WHERE job_id = 'SA_REP'
       AND commission_pct < .2;

Deleting Rows from a Remote Database: Example

The following statement deletes specified rows from the `locations` table
owned by the user `hr` on a database accessible by the database link `remote`:

    
    
    DELETE FROM hr.locations@remote
       WHERE location_id > 3000;

Deleting Nested Table Rows: Example

For an example that deletes nested table rows, refer to "[Table Collections:
Examples](SELECT.md#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6__I2071643)".

Deleting Rows from a Partition: Example

The following example removes rows from partition `sales_q1_1998` of the
`sh.sales` table:

    
    
    DELETE FROM sales PARTITION (sales_q1_1998)
       WHERE amount_sold > 1000;

Using the RETURNING Clause: Example

The following example returns column `salary` from the deleted rows and stores
the result in bind variable `:bnd1`. The bind variable must already have been
declared.

    
    
    DELETE FROM employees
       WHERE job_id = 'SA_REP' 
       AND hire_date + TO_YMINTERVAL('01-00') < SYSDATE 
       RETURNING salary INTO :bnd1;

Deleting Data from a Table: Example

The following statements create a table named product_price_history and insert
data into it:

    
    
    CREATE TABLE product_price_history ( 
      product_id          INTEGER NOT NULL, 
      price               INTEGER NOT NULL, 
      currency_code       VARCHAR2(3 CHAR) NOT NULL, 
      effective_from_date DATE NOT NULL, 
      effective_to_date   DATE, 
      CONSTRAINT product_price_history_pk 
        PRIMARY KEY (product_id, currency_code, effective_from_date) 
    ) PARTITION BY RANGE (effective_from_date) ( 
        PARTITION p0 VALUES less than (DATE'2015-01-02'), 
        PARTITION p1 VALUES less than (DATE'2015-01-03'), 
        PARTITION p2 VALUES less than (DATE'2015-01-04') 
    );
    
    INSERT INTO product_price_history 
      WITH prices AS ( 
        SELECT 1, 100, 'USD', DATE'2015-01-01', DATE'2015-01-02' 
        FROM   dual UNION ALL 
        SELECT 1, 60, 'GBP', DATE'2015-01-01', DATE'2015-01-02' 
        FROM   dual UNION ALL 
        SELECT 1, 110, 'EUR', DATE'2015-01-01', DATE'2015-01-02' 
        FROM   dual UNION ALL 
        SELECT 1, 101, 'USD', DATE'2015-01-02', DATE'2015-01-03' 
        FROM   dual UNION ALL 
        SELECT 1, 62, 'GBP', DATE'2015-01-02', DATE'2015-01-03' 
        FROM   dual UNION ALL 
        SELECT 1, 109, 'EUR', DATE'2015-01-02', DATE'2015-01-03' 
        FROM   dual UNION ALL 
        SELECT 1, 105, 'USD', DATE'2015-01-03', NULL 
        FROM   dual UNION ALL 
        SELECT 1, 61, 'GBP', DATE'2015-01-03', NULL 
        FROM   dual UNION ALL 
        SELECT 1, 107, 'EUR', DATE'2015-01-03', NULL 
        FROM   dual UNION ALL 
        SELECT 2, 30, 'USD', DATE'2015-01-01', DATE'2015-01-03' 
        FROM   dual UNION ALL 
        SELECT 2, 33, 'USD', DATE'2015-01-03', NULL 
        FROM   dual UNION ALL 
        SELECT 3, 100, 'GBP', DATE'2015-01-03', NULL 
        FROM   dual 
      ) 
    SELECT * 
    FROM   prices;

The following statement deletes the rows from the table product_price_history
where product_id is 3:

    
    
    DELETE FROM product_price_history WHERE product_id = 3;

The following procedure deletes the rows from the product_price_history where
product_id is 2 and effective_to_date is NULL:

    
    
    DECLARE 
      currency product_price_history.currency_code%TYPE; 
    BEGIN 
      DELETE product_price_history 
      WHERE  product_id = 2 
      AND    effective_to_date IS NULL 
      returning currency_code INTO currency; 
          
      dbms_output.Put_line(currency); 
    END;
    
    USD 

The following statement deletes the rows from the table product_price_history
where currency_code is âEURâ:

    
    
    DELETE (SELECT * FROM product_price_history) WHERE  currency_code = 'EUR';
    

The following statement uses a subquery to delete rows from
product_price_history:

    
    
    DELETE product_price_history pp 
    WHERE  (product_id, currency_code, effective_from_date) 
       IN (SELECT product_id, currency_code, Max(effective_from_date) 
           FROM   product_price_history 
           GROUP BY product_id, currency_code);

The following statement uses partitions to delete rows from
product_price_history:

    
    
    DELETE product_price_history partition (p1);

The following statement displays the table information:

    
    
    SELECT * FROM product_price_history;
    
    PRODUCT_ID	PRICE CUR EFFECTIVE EFFECTIVE
    ---------- ---------- --- --------- ---------
    	 1	  100 USD 01-JAN-15 02-JAN-15
    	 1	   60 GBP 01-JAN-15 02-JAN-15

The following statement deletes all rows from product_price_history:

    
    
    DELETE product_price_history;


[← Previous](CREATE-VIEW.md)

[Next →](DISASSOCIATE-STATISTICS.md)
