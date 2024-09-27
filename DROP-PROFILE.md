[Previous](DROP-PROCEDURE.md) [Next](drop-property-graph.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP PROFILE 

## DROP PROFILE

Purpose

Use the `DROP` `PROFILE` statement to remove a profile from the database. You
can drop any profile except the `DEFAULT` profile.

See Also:

[CREATE PROFILE](CREATE-PROFILE.md#GUID-
ABC7AE4D-64A8-4EA9-857D-BEF7300B64C3) and [ALTER PROFILE](ALTER-
PROFILE.md#GUID-7D2EA18A-49F9-40FA-ADE8-BB3D5D5FE4A1) on creating and
modifying a profile

Prerequisites

You must have the `DROP` `PROFILE` system privilege.

Syntax

drop_profile::=

![Description of drop_profile.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_profile.gif)  
[Description of the illustration drop_profile.eps](img_text/drop_profile.md)

Semantics

profile

Specify the name of the profile to be dropped.

CASCADE

Specify `CASCADE` to deassign the profile from any users to whom it is
assigned. Oracle Database automatically assigns the `DEFAULT` profile to such
users. You must specify this clause to drop a profile that is currently
assigned to users.

Examples

Dropping a Profile: Example

The following statement drops the profile `app_user`, which was created in
"[Creating a Profile: Example](CREATE-PROFILE.md#GUID-
ABC7AE4D-64A8-4EA9-857D-BEF7300B64C3__I2092094)". Oracle Database drops the
profile `app_user` and assigns the `DEFAULT` profile to any users currently
assigned the `app_user` profile:

    
    
    DROP PROFILE app_user CASCADE; 


[← Previous](DROP-PROCEDURE.md)

[Next →](drop-property-graph.md)
