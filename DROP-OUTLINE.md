[Previous](DROP-OPERATOR.md) [Next](DROP-PACKAGE.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP OUTLINE 

## DROP OUTLINE

Purpose

Note:

  * Stored outlines are deprecated. They are still supported for backward compatibility. However, Oracle recommends that you use SQL plan management instead. SQL plan management creates SQL plan baselines, which offer superior SQL performance stability compared with stored outlines.

  * You can migrate existing stored outlines to SQL plan baselines by using the `MIGRATE_STORED_OUTLINE` function of the `DBMS_SPM` package or Enterprise Manager Cloud Control. When the migration is complete, the stored outlines are marked as migrated and can be removed. You can drop all migrated stored outlines on your system by using the `DROP_MIGRATED_STORED_OUTLINE` function of the `DBMS_SPM` package. 

  * See Also: [Oracle Database SQL Tuning Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=TGSQL615) for more information about SQL plan management and [Oracle Database PL/SQL Packages and Types Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS150) for information about the `DBMS_SPM` package 

Use the `DROP` `OUTLINE` statement to drop a stored outline.

See Also:

[CREATE OUTLINE](CREATE-OUTLINE.md#GUID-7CC033AF-
DB19-4616-87D9-8173939FD627) for information on creating an outline

Prerequisites

To drop an outline, you must have the `DROP` `ANY` `OUTLINE` system privilege.

Syntax

drop_outline::=

![Description of drop_outline.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_outline.gif)  
[Description of the illustration drop_outline.eps](img_text/drop_outline.md)

Semantics

outline

Specify the name of the outline to be dropped.

After the outline is dropped, if the SQL statement for which the stored
outline was created is compiled, then the optimizer generates a new execution
plan without the influence of the outline.

Examples

Dropping an Outline: Example

The following statement drops the stored outline called `salaries`.

    
    
    DROP OUTLINE salaries;


[← Previous](DROP-OPERATOR.md)

[Next →](DROP-PACKAGE.md)
