[Previous](ALTER-OPERATOR.md) [Next](ALTER-PACKAGE.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ALTER LIBRARY to ALTER SESSION](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
  3. ALTER OUTLINE 

## ALTER OUTLINE

Purpose

Note:

Stored outlines are deprecated. They are still supported for backward
compatibility. However, Oracle recommends that you use SQL plan management
instead. SQL plan management creates SQL plan baselines, which offer superior
SQL performance stability compared with stored outlines.

You can migrate existing stored outlines to SQL plan baselines by using the
`MIGRATE_STORED_OUTLINE` function of the `DBMS_SPM` package or Enterprise
Manager Cloud Control. When the migration is complete, the stored outlines are
marked as migrated and can be removed. You can drop all migrated stored
outlines on your system by using the `DROP_MIGRATED_STORED_OUTLINE` function
of the `DBMS_SPM` package.

See Also:â[Oracle Database SQL Tuning
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=TGSQL615) for more information about SQL plan management
and [Oracle Database PL/SQL Packages and Types
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ARPLS150) for information about the `DBMS_SPM` package

Use the `ALTER` `OUTLINE` statement to rename a stored outline, reassign it to
a different category, or regenerate it by compiling the outline's SQL
statement and replacing the old outline data with the outline created under
current conditions.

See Also:

[CREATE OUTLINE](CREATE-OUTLINE.md#GUID-7CC033AF-
DB19-4616-87D9-8173939FD627) for information on creating an outline

Prerequisites

To modify an outline, you must have the `ALTER` `ANY` `OUTLINE` system
privilege.

Syntax

alter_outline::=

![Description of alter_outline.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_outline.gif)  
[Description of the illustration
alter_outline.eps](img_text/alter_outline.md)

Semantics

PUBLIC | PRIVATE 

Specify `PUBLIC` if you want to modify the public version of this outline.
This is the default.

Specify `PRIVATE` if you want to modify an outline that is private to the
current session and whose data is stored in the current parsing schema.

outline

Specify the name of the outline to be modified.

REBUILD

Specify `REBUILD` to regenerate the execution plan for `outline` using current
conditions.

See Also:

"[Rebuilding an Outline: Example](ALTER-
OUTLINE.md#GUID-49F25C82-0783-4407-88BB-613F986C2FEC__I2227342)"

RENAME TO Clause

Use the `RENAME` `TO` clause to specify an outline name to replace `outline`.

CHANGE CATEGORY TO Clause

Use the `CHANGE` `CATEGORY` `TO` clause to specify the name of the category
into which the `outline` will be moved.

ENABLE | DISABLE

Use this clause to selectively enable or disable this outline. Outlines are
enabled by default. The `DISABLE` keyword lets you disable one outline without
affecting the use of other outlines.

Examples

Rebuilding an Outline: Example

The following statement regenerates a stored outline called `salaries` by
compiling the text of the outline and replacing the old outline data with the
outline created under current conditions.

    
    
    ALTER OUTLINE salaries REBUILD;


[← Previous](ALTER-OPERATOR.md)

[Next →](ALTER-PACKAGE.md)
