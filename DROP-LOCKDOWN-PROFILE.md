[Previous](DROP-LIBRARY.md) [Next](DROP-MATERIALIZED-VIEW.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP LOCKDOWN PROFILE

## DROP LOCKDOWN PROFILE

Purpose

Use the `DROP` `LOCKDOWN` `PROFILE` statement to remove a PDB lockdown profile
from the database. A PDB that was assigned the dropped profile will continue
to be assigned the profile, but will not be subject to the restrictions
imposed by the dropped profile.

If the `PDB_LOCKDOWN` initialization parameter for a CDB, an application root,
or a PDB has the value of the dropped lockdown profile, then the restrictions
imposed by the dropped profile will be disabled when you drop it. However, the
value of the `PDB_LOCKDOWN` initialization parameter will remain until you
explicitly unset it.

See Also:

  * [CREATE LOCKDOWN PROFILE](CREATE-LOCKDOWN-PROFILE.md#GUID-1CDEC3A3-F3F1-4279-9370-36AACF416E0A) and [ALTER LOCKDOWN PROFILE](ALTER-LOCKDOWN-PROFILE.md#GUID-B4029154-54A8-4B78-97C3-9CED416F1C34)

  * [Oracle Database Security Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DBSEG-GUID-AB5E62DB-7E2A-4B5A-BA96-A2BD2DF15275) for more information on PDB lockdown profiles 

Prerequisites

  * You must issue this statement from the CDB Root or the Application Root. 

  * You must have the `DROP` `LOCKDOWN` `PROFILE` system privilege in the container where you mean to issue the statement. 

Syntax

drop_lockdown_profile::=

![Description of drop_lockdown_profile.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_lockdown_profile.gif)  
[Description of the illustration
drop_lockdown_profile.eps](img_text/drop_lockdown_profile.md)

Semantics

profile_name

Specify the name of the PDB lockdown profile to be dropped.

You can find the names of existing PDB lockdown profiles by querying the
`DBA_LOCKDOWN_PROFILES` data dictionary view.

See Also:

Oracle Database Reference for more information on the
[`DBA_LOCKDOWN_PROFILES`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN-GUID-2DEBBEBC-7A6B-4984-A7E7-90314971182E) data
dictionary view and the
[`PDB_LOCKDOWN`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN-GUID-27072E94-1E1D-4BB0-AEAE-D7AFDC02E0A1)
initialization parameter

Example

The following statement drops PDB lockdown profile `hr_prof`:

    
    
    DROP LOCKDOWN PROFILE hr_prof;


[← Previous](DROP-LIBRARY.md)

[Next →](DROP-MATERIALIZED-VIEW.md)
