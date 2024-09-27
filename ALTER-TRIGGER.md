[Previous](ALTER-TABLESPACE-SET.md) [Next](ALTER-TYPE.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: ALTER SYNONYM to COMMENT](SQL-Statements-ALTER-SYNONYM-to-COMMENT.md)
  3. ALTER TRIGGER 

## ALTER TRIGGER

Purpose

Triggers are defined using PL/SQL. Therefore, this section provides some
general information but refers to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS99996) for details of syntax and semantics.

Use the `ALTER` `TRIGGER` statement to enable, disable, or compile a database
trigger.

Note:

This statement does not change the declaration or definition of an existing
trigger. To redeclare or redefine a trigger, use the `CREATE` `TRIGGER`
statement with the `OR` `REPLACE` keywords.

See Also:

  * [CREATE TRIGGER](CREATE-TRIGGER.md#GUID-EE0DF3AA-7ADC-4171-B8E8-138BE9224E3B) for information on creating a trigger 

  * [DROP TRIGGER](DROP-TRIGGER.md#GUID-724AC8BC-0428-43D3-8F11-4D4AD8DC2984) for information on dropping a trigger 

  * [Oracle Database Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=CNCPT118) for general information on triggers 

Prerequisites

The trigger must be in your own schema or you must have `ALTER` `ANY`
`TRIGGER` system privilege.

In addition, to alter a trigger on `DATABASE`, you must have the `ADMINISTER`
`DATABASE` `TRIGGER` privilege.

See Also:

[CREATE TRIGGER](CREATE-TRIGGER.md#GUID-
EE0DF3AA-7ADC-4171-B8E8-138BE9224E3B) for more information on triggers based
on `DATABASE` triggers

Syntax

alter_trigger::=

![Description of alter_trigger.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_trigger.gif)  
[Description of the illustration
alter_trigger.eps](img_text/alter_trigger.md)

(`trigger_compile_clause`: See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS1896) for the syntax of this clause.)

Semantics

IF EXISTS

Specify `IF EXISTS` to alter an existing table.

Specifying `IF NOT EXISTS` with `ALTER VIEW` results in `ORA-11544: Incorrect
IF EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the trigger. If you omit `schema`, then Oracle
Database assumes the trigger is in your own schema.

trigger_name

Specify the name of the trigger to be altered.

trigger_compile_clause

See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS1896) for the syntax and semantics of this clause
and for complete information on creating and compiling triggers.

ENABLE | DISABLE

Specify `ENABLE` to enable the trigger. You can also use the `ENABLE` `ALL`
`TRIGGERS` clause of `ALTER` `TABLE` to enable all triggers associated with a
table. See [ALTER TABLE](ALTER-
TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877).

Specify `DISABLE` to disable the trigger. You can also use the `DISABLE` `ALL`
`TRIGGERS` clause of `ALTER` `TABLE` to disable all triggers associated with a
table.

RENAME Clause

Specify `RENAME` `TO` `new_name` to rename the trigger. Oracle Database
renames the trigger and leaves it in the same state it was in before being
renamed.

When you rename a trigger, the database rebuilds the remembered source of the
trigger in the `USER_SOURCE`, `ALL_SOURCE`, and `DBA_SOURCE` data dictionary
views. As a result, comments and formatting may change in the `TEXT` column of
those views even though the trigger source did not change.

EDITIONABLE | NONEDITIONABLE

Use these clauses to specify whether the trigger becomes an editioned or
noneditioned object if editioning is later enabled for the schema object type
`TRIGGER` in `schema`. The default is `EDITIONABLE`. For information about
altering editioned and noneditioned objects, see [Oracle Database Development
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADFNS1287).

Restriction on NONEDITIONABLE

You cannot specify `NONEDITIONABLE` for a crossedition trigger.


[← Previous](ALTER-TABLESPACE-SET.md)

[Next →](ALTER-TYPE.md)
