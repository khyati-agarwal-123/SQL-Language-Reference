[Previous](DROP-VIEW.md) [Next](FLASHBACK-DATABASE.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: DROP TABLE to LOCK TABLE](SQL-Statements-DROP-TABLE-to-LOCK-TABLE.md)
  3. EXPLAIN PLAN 

## EXPLAIN PLAN

Purpose

Use the `EXPLAIN` `PLAN` statement to determine the execution plan Oracle
Database follows to execute a specified SQL statement. This statement inserts
a row describing each step of the execution plan into a specified table. You
can also issue the `EXPLAIN` `PLAN` statement as part of the SQL trace
facility.

This statement also determines the cost of executing the statement. If any
domain indexes are defined on the table, then user-defined CPU and I/O costs
will also be inserted.

The definition of a sample output table `PLAN_TABLE` is available in a SQL
script on your distribution media. Your output table must have the same column
names and data types as this table. The common name of this script is
`UTLXPLAN.SQL`. The exact name and location depend on your operating system.

Oracle Database provides information on cached cursors through several dynamic
performance views:

  * For information on the work areas used by SQL cursors, query `V$SQL_WORKAREA`. 

  * For information on the execution plan for a cached cursor, query `V$SQL_PLAN`. 

  * For execution statistics at each step or operation of an execution plan of cached cursors (for example, number of produced rows, number of blocks read), query `V$SQL_PLAN_STATISTICS`. 

  * For a selective precomputed join of the preceding three views, query `V$SQL_PLAN_STATISTICS_ALL`. 

  * Execution statistics at each step or operation of an execution plan of cached cursors are displayed in `V$SQL_PLAN_MONITOR` if the statement execution is monitored. You can force monitoring using the `MONITOR` hint. 

See Also:

  * [Oracle Database SQL Tuning Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=TGSQL271) for information on the output of `EXPLAIN` `PLAN`, how to use the SQL trace facility, and how to generate and interpret execution plans 

  * [Oracle Database Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN003) for information on dynamic performance views 

Prerequisites

To issue an `EXPLAIN` `PLAN` statement, you must have the privileges necessary
to insert rows into an existing output table that you specify to hold the
execution plan.

You must also have the privileges necessary to execute the SQL statement for
which you are determining the execution plan. If the SQL statement accesses a
view, then you must have privileges to access any tables and views on which
the view is based. If the view is based on another view that is based on a
table, then you must have privileges to access both the other view and its
underlying table.

To examine the execution plan produced by an `EXPLAIN` `PLAN` statement, you
must have the privileges necessary to query the output table.

The `EXPLAIN` `PLAN` statement is a data manipulation language (DML)
statement, rather than a data definition language (DDL) statement. Therefore,
Oracle Database does not implicitly commit the changes made by an `EXPLAIN`
`PLAN` statement. If you want to keep the rows generated by an `EXPLAIN`
`PLAN` statement in the output table, then you must commit the transaction
containing the statement.

See Also:

[INSERT](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423) and
[SELECT](SELECT.md#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6) for
information on the privileges you need to populate and query the plan table

Syntax

explain_plan::=

![Description of explain_plan.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/explain_plan.gif)  
[Description of the illustration explain_plan.eps](img_text/explain_plan.md)

Semantics

SET STATEMENT_ID Clause

Specify a value for the `STATEMENT_ID` column for the rows of the execution
plan in the output table. You can then use this value to identify these rows
among others in the output table. Be sure to specify a `STATEMENT_ID` value if
your output table contains rows from many execution plans. If you omit this
clause, then the `STATEMENT_ID` value defaults to null.

INTO table Clause

Specify the name of the output table, and optionally its schema and database.
This table must exist before you use the `EXPLAIN` `PLAN` statement.

If you omit `schema`, then the database assumes the table is in your own
schema.

The `dblink` can be a complete or partial name of a database link to a remote
Oracle Database where the output table is located. You can specify a remote
output table only if you are using Oracle Database distributed functionality.
If you omit `dblink`, then the database assumes the table is on your local
database. See "[References to Objects in Remote Databases](Syntax-for-Schema-
Objects-and-Parts-in-SQL-
Statements.md#GUID-61D0B206-A5EA-473F-AD04-7067D6E3914C)" for information on
referring to database links.

If you omit `INTO` altogether, then the database assumes an output table named
`PLAN_TABLE` in your own schema on your local database.

FOR statement Clause

Specify a `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `MERGE`, `CREATE` `TABLE`,
`CREATE` `INDEX`, or `ALTER` `INDEX` ... `REBUILD` statement for which the
execution plan is generated.

Notes on EXPLAIN PLAN

The following notes apply to `EXPLAIN` `PLAN`:

  * If `statement` includes the `parallel_clause`, then the resulting execution plan will indicate parallel execution. However, `EXPLAIN` `PLAN` actually inserts the statement into the plan table, so that the parallel DML statement you submit is no longer the first DML statement in the transaction. This violates the Oracle Database restriction of one parallel DML statement in a single transaction, and the statement will be executed serially. To maintain parallel execution of the statements, you must commit or roll back the `EXPLAIN` `PLAN` statement, and then submit the parallel DML statement. 

  * To determine the execution plan for an operation on a temporary table, `EXPLAIN` `PLAN` must be run from the same session, because the data in temporary tables is session specific. 

Examples

EXPLAIN PLAN Examples

The following statement determines the execution plan and cost for an `UPDATE`
statement and inserts rows describing the execution plan into the specified
`plan_table` table with the `STATEMENT_ID` value of 'Raise in Tokyo':

    
    
    EXPLAIN PLAN 
        SET STATEMENT_ID = 'Raise in Tokyo' 
        INTO plan_table 
        FOR UPDATE employees 
            SET salary = salary * 1.10 
            WHERE department_id =  
               (SELECT department_id FROM departments
                   WHERE location_id = 1700); 
    

The following `SELECT` statement queries the `plan_table` table and returns
the execution plan and the cost:

    
    
    SELECT id, LPAD(' ',2*(LEVEL-1))||operation operation, options,
           object_name, object_alias, position 
        FROM plan_table 
        START WITH id = 0 AND statement_id = 'Raise in Tokyo'
        CONNECT BY PRIOR id = parent_id AND statement_id = 'Raise in Tokyo'
        ORDER BY id;
    

The query returns this execution plan:

    
    
     ID OPERATION            OPTIONS              OBJECT_NAME          OBJECT_ALIAS         POSITION
    --- -------------------- -------------------- -------------------- -------------------- --------
      0 UPDATE STATEMENT                                                                           4
      1   UPDATE                                  EMPLOYEES                                        1
      2     INDEX            RANGE SCAN           EMP_DEPARTMENT_IX    EMPLOYEES@UPD$1             1
      3       TABLE ACCESS   BY INDEX ROWID       DEPARTMENTS          DEPARTMENTS@SEL$1           1
      4         INDEX        RANGE SCAN           DEPT_LOCATION_IX     DEPARTMENTS@SEL$1           1
    

The value in the `POSITION` column of the first row shows that the statement
has a cost of 4.

EXPLAIN PLAN: Partitioned Example

The sample table `sh.sales` is partitioned on the `time_id` column. Partition
`sales_q3_2000` contains time values less than Oct. 1, 2000, and there is a
local index `sales_time_bix` on the `time_id` column.

Consider the query:

    
    
    EXPLAIN PLAN FOR
      SELECT * FROM sales 
         WHERE time_id BETWEEN :h AND '01-OCT-2000';
    

where `:h` represents an already declared bind variable. `EXPLAIN`` PLAN`
executes this query with `PLAN_TABLE` as the output table. The basic execution
plan, including partitioning information, is obtained with the following
query:

    
    
    SELECT operation, options, partition_start, partition_stop,
           partition_id
      FROM plan_table;


[← Previous](DROP-VIEW.md)

[Next →](FLASHBACK-DATABASE.md)
