[Previous](DELETE.md) [Next](DROP-ANALYTIC-VIEW.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: CREATE SEQUENCE to DROP CLUSTER](SQL-Statements-CREATE-SEQUENCE-to-DROP-CLUSTER.md)
  3. DISASSOCIATE STATISTICS 

## DISASSOCIATE STATISTICS

Purpose

Use the `DISASSOCIATE` `STATISTICS` statement to disassociate default
statistics or a statistics type from columns, standalone functions, packages,
types, domain indexes, or indextypes.

See Also:

[ASSOCIATE STATISTICS](ASSOCIATE-STATISTICS.md#GUID-
BD02BA6A-32A7-4093-A6B6-BAE860C0F834) for more information on statistics type
associations

Prerequisites

To issue this statement, you must have the appropriate privileges to alter the
underlying table, function, package, type, domain index, or indextype.

Syntax

disassociate_statistics::=

![Description of disassociate_statistics.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/disassociate_statistics.gif)  
[Description of the illustration
disassociate_statistics.eps](img_text/disassociate_statistics.md)

Semantics

FROM COLUMNS | FUNCTIONS | PACKAGES | TYPES | INDEXES | INDEXTYPES

Specify one or more columns, standalone functions, packages, types, domain
indexes, or indextypes from which you are disassociating statistics.

If you do not specify `schema`, then Oracle Database assumes the object is in
your own schema.

If you have collected user-defined statistics on the object, then the
statement fails unless you specify `FORCE`.

FORCE

Specify `FORCE` to remove the association regardless of whether any statistics
exist for the object using the statistics type. If statistics do exist, then
the statistics are deleted before the association is deleted.

Note:

When you drop an object with which a statistics type has been associated,
Oracle Database automatically disassociates the statistics type with the
`FORCE` option and drops all statistics that have been collected with the
statistics type.

Examples

Disassociating Statistics: Example

This statement disassociates statistics from the `emp_mgmt` package. See
[Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01378) for the example that creates this package in
the `hr` schema.

    
    
    DISASSOCIATE STATISTICS FROM PACKAGES hr.emp_mgmt;


[← Previous](DELETE.md)

[Next →](DROP-ANALYTIC-VIEW.md)
