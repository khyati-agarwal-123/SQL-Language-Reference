[Previous](DROP-RESTORE-POINT.md) [Next](DROP-ROLLBACK-SEGMENT.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP ROLE 

## DROP ROLE

Purpose

Use the `DROP` `ROLE` statement to remove a role from the database. When you
drop a role, Oracle Database revokes it from all users and roles to whom it
has been granted and removes it from the database. User sessions in which the
role is already enabled are not affected. However, no new user session can
enable the role after it is dropped.

See Also:

  * [CREATE ROLE](CREATE-ROLE.md#GUID-B2252DC5-5AE7-49B7-9048-98062993E450) and [ALTER ROLE](ALTER-ROLE.md#GUID-85543272-EAF4-4FED-A921-AD9868102C39) for information on creating roles and changing the authorization needed to enable a role 

  * [SET ROLE](SET-ROLE.md#GUID-863F9B6F-82B4-4C49-8E3A-3BA33AE79CAB) for information on disabling roles for the current session 

Prerequisites

You must have been granted the role with the `ADMIN` `OPTION` or you must have
the `DROP` `ANY` `ROLE` system privilege.

Syntax

drop_role::=

![Description of drop_role.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_role.gif)  
[Description of the illustration drop_role.eps](img_text/drop_role.md)

Semantics

role

Specify the name of the role to be dropped.

Examples

Dropping a Role: Example

To drop the role `dw_manager`, which was created in "[Creating a Role:
Example](CREATE-
ROLE.md#GUID-B2252DC5-5AE7-49B7-9048-98062993E450__I2082342)", issue the
following statement:

    
    
    DROP ROLE dw_manager; 


[← Previous](DROP-RESTORE-POINT.md)

[Next →](DROP-ROLLBACK-SEGMENT.md)
