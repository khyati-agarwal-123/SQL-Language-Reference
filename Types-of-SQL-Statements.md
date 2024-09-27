[Previous](SQL-Statements-ADMINISTER-KEY-MANAGEMENT-to-ALTER-JAVA.md)
[Next](How-the-SQL-Statement-Chapters-are-Organized.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ADMINISTER KEY MANAGEMENT to ALTER JAVA](SQL-Statements-ADMINISTER-KEY-MANAGEMENT-to-ALTER-JAVA.md)
  3. Types of SQL Statements 

## Types of SQL Statements

The lists in the following sections provide a functional summary of SQL
statements and are divided into these categories:

  * [Data Definition Language (DDL) Statements](Types-of-SQL-Statements.md#GUID-FD9A8CB4-6B9A-44E5-B114-EFB8DA76FC88)

  * [Data Manipulation Language (DML) Statements](Types-of-SQL-Statements.md#GUID-2E008D4A-F6FD-4F34-9071-7E10419CA24D)

  * [Transaction Control Statements](Types-of-SQL-Statements.md#GUID-FEC504E9-D22D-4082-A092-07891911C5CF)

  * [Session Control Statements](Types-of-SQL-Statements.md#GUID-B8AEC1B3-D1E8-4567-9EFB-8F3410CA70A4)

  * [System Control Statement](Types-of-SQL-Statements.md#GUID-83CC2729-F33B-45D8-A6C5-0D3C654FBFC4)

  * [Embedded SQL Statements](Types-of-SQL-Statements.md#GUID-CD76B6B5-01C4-46CA-964A-A41872D6AEB0)

### Data Definition Language (DDL) Statements

Data definition language (DDL) statements let you to perform these tasks:

  * Create, alter, and drop schema objects 

  * Grant and revoke privileges and roles 

  * Analyze information on a table, index, or cluster

  * Establish auditing options 

  * Add comments to the data dictionary 

The `CREATE`, `ALTER`, and `DROP` commands require exclusive access to the
specified object. For example, an `ALTER` `TABLE` statement fails if another
user has an open transaction on the specified table.

The `GRANT`, `REVOKE`, `ANALYZE`, `AUDIT`, and `COMMENT` commands do not
require exclusive access to the specified object. For example, you can analyze
a table while other users are updating the table.

Oracle Database implicitly commits the current transaction before and after
every DDL statement.

A DDL statement is either blocking or nonblocking, and both types of DDL
statements require exclusive locks on internal structures.

See Also:

[Oracle Database Development
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADFNS187) to learn about the difference between blocking
and nonblocking DDL

Many DDL statements may cause Oracle Database to recompile or reauthorize
schema objects. For information on how Oracle Database recompiles and
reauthorizes schema objects and the circumstances under which a DDL statement
would cause this, see [Oracle Database
Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=CNCPT216).

DDL statements are supported by PL/SQL with the use of the `DBMS_SQL` package.

See Also:

[Oracle Database PL/SQL Packages and Types
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ARPLS058) for more information about this package

The DDL statements are:

  * `ALTER` ... (All statements beginning with `ALTER`, except `ALTER` `SESSION` and `ALTER` `SYSTEM`âsee "[Session Control Statements](Types-of-SQL-Statements.md#GUID-B8AEC1B3-D1E8-4567-9EFB-8F3410CA70A4)" and "[System Control Statement](Types-of-SQL-Statements.md#GUID-83CC2729-F33B-45D8-A6C5-0D3C654FBFC4)") 
  * `ANALYZE`
  * `ASSOCIATE` `STATISTICS`
  * `AUDIT`
  * `COMMENT`
  * `CREATE` ... (All statements beginning with `CREATE)`
  * `DISASSOCIATE` `STATISTICS`
  * `DROP` ... (All statements beginning with `DROP)`
  * `FLASHBACK` ... (All statements beginning with `FLASHBACK`) 
  * `GRANT`
  * `NOAUDIT`
  * `PURGE`
  * `RENAME`
  * `REVOKE`
  * `TRUNCATE`

### Data Manipulation Language (DML) Statements

Data manipulation language (DML) statements access and manipulate data in
existing schema objects. These statements do not implicitly commit the current
transaction. The data manipulation language statements are:

  * `CALL`
  * `DELETE`
  * `EXPLAIN PLAN`
  * `INSERT`
  * `LOCK TABLE`
  * `MERGE`
  * `SELECT`
  * `UPDATE`

The `SELECT` statement is a limited form of DML statement in that it can only
access data in the database. It cannot manipulate data stored in the database,
although it can manipulate the accessed data before returning the results of
the query.

The `SELECT` statement is supported in PL/SQL only when executed dynamically.
However, you can use the similar PL/SQL statement [`SELECT`
`INTO`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01345) in PL/SQL code, and you do not have to
execute it dynamically. The `CALL` and `EXPLAIN` `PLAN` statements are
supported in PL/SQL only when executed dynamically. All other DML statements
are fully supported in PL/SQL.

### Transaction Control Statements

Transaction control statements manage changes made by DML statements. The
transaction control statements are:

  * `COMMIT`
  * `ROLLBACK`
  * `SAVEPOINT`
  * `SET` `TRANSACTION`
  * `SET` `CONSTRAINT`

All transaction control statements, except certain forms of the `COMMIT` and
`ROLLBACK` commands, are supported in PL/SQL. For information on the
restrictions, see
[COMMIT](COMMIT.md#GUID-6CD5C9A7-54B9-4FA2-BA3C-D6B4492B9EE2) and
[ROLLBACK](ROLLBACK.md#GUID-94551F0C-A47F-43DE-BC68-9B1C1ED38C93).

### Session Control Statements

Session control statements dynamically manage the properties of a user
session. These statements do not implicitly commit the current transaction.

PL/SQL does not support session control statements. The session control
statements are:

  * `ALTER SESSION`
  * `SET ROLE`

### System Control Statement

The single system control statement, `ALTER` `SYSTEM`, dynamically manages the
properties of an Oracle Database instance. This statement does not implicitly
commit the current transaction and is not supported in PL/SQL.

### Embedded SQL Statements

Embedded SQL statements place DDL, DML, and transaction control statements
within a procedural language program. Embedded SQL is supported by the Oracle
precompilers and is documented in the following books:

  * [Pro*COBOL Programmer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=LNPCB005)

  * [Pro*C/C++ Programmer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=LNPCC3339)


[← Previous](Types-of-SQL-Statements.md)

[Next →](How-the-SQL-Statement-Chapters-are-Organized.md)
