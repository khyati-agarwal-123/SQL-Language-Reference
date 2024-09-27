[Previous](ALTER-PROCEDURE.md) [Next](alter-property-graph.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ALTER LIBRARY to ALTER SESSION](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
  3. ALTER PROFILE 

## ALTER PROFILE

Purpose

Use the `ALTER` `PROFILE` statement to add, modify, or remove a resource limit
or password management parameter in a profile.

Changes made to a profile with an `ALTER` `PROFILE` statement affect users
only in their subsequent sessions, not in their current sessions.

See Also:

[CREATE PROFILE](CREATE-PROFILE.md#GUID-
ABC7AE4D-64A8-4EA9-857D-BEF7300B64C3) for information on creating a profile

Prerequisites

You must have the `ALTER` `PROFILE` system privilege.

To specify the `CONTAINER` clause, you must be connected to a multitenant
container database (CDB). To specify `CONTAINER` `=` `ALL`, the current
container must be the root. To specify `CONTAINER` `=` `CURRENT`, the current
container must be a pluggable database (PDB).

Syntax

alter_profile::=

![Description of alter_profile.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_profile.gif)  
[Description of the illustration
alter_profile.eps](img_text/alter_profile.md)

([resource_parameters::=](ALTER-PROFILE.md#GUID-7D2EA18A-49F9-40FA-
ADE8-BB3D5D5FE4A1__I2282119), [password_parameters::=](ALTER-
PROFILE.md#GUID-7D2EA18A-49F9-40FA-ADE8-BB3D5D5FE4A1__I2282087))

resource_parameters::=

![Description of resource_parameters.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/resource_parameters.gif)  
[Description of the illustration
resource_parameters.eps](img_text/resource_parameters.md)

([size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID))

password_parameters::=

![Description of password_parameters.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/password_parameters.gif)  
[Description of the illustration
password_parameters.eps](img_text/password_parameters.md)

Semantics

The keywords, parameters, and clauses common to `ALTER` `PROFILE` and `CREATE`
`PROFILE` have the same meaning. For full semantics of these keywords,
parameters, and clauses refer to [CREATE PROFILE](CREATE-PROFILE.md#GUID-
ABC7AE4D-64A8-4EA9-857D-BEF7300B64C3) .

Only common users who have been commonly granted the `ALTER PROFILE` system
privilege can alter or drop the mandatory profile, and only from the CDB root.

You cannot remove a limit from the `DEFAULT` profile.

Examples

Making a Password Unavailable: Example

The following statement makes the password of the `new_profile` profile
(created in "[Creating a Profile: Example](CREATE-PROFILE.md#GUID-
ABC7AE4D-64A8-4EA9-857D-BEF7300B64C3__I2092094)") unavailable for reuse for 90
days:

    
    
    ALTER PROFILE new_profile 
       LIMIT PASSWORD_REUSE_TIME 90 
       PASSWORD_REUSE_MAX UNLIMITED;

Setting Default Password Values: Example

The following statement defaults the `PASSWORD_REUSE_TIME` value of the
`app_user` profile (created in "[Setting Profile Resource Limits:
Example](CREATE-PROFILE.md#GUID-
ABC7AE4D-64A8-4EA9-857D-BEF7300B64C3__I2120023)") to its defined value in the
`DEFAULT` profile:

    
    
    ALTER PROFILE app_user 
       LIMIT PASSWORD_REUSE_TIME DEFAULT
       PASSWORD_REUSE_MAX UNLIMITED;

Limiting Login Attempts and Password Lock Time: Example

The following statement alters profile `app_user` with `FAILED_LOGIN_ATTEMPTS`
set to 5 and `PASSWORD_LOCK_TIME` set to 1:

    
    
    ALTER PROFILE app_user LIMIT
       FAILED_LOGIN_ATTEMPTS 5
       PASSWORD_LOCK_TIME 1;
    

This statement causes any user account to which the `app_user` profile is
assigned to become locked for one day after five consecutive unsuccessful
login attempts.

Changing Password Lifetime and Grace Period: Example

The following statement modifies the profile `app_user2` `PASSWORD_LIFE_TIME`
to 90 days and `PASSWORD_GRACE_TIME` to 5 days:

    
    
    ALTER PROFILE app_user2 LIMIT
       PASSWORD_LIFE_TIME 90
       PASSWORD_GRACE_TIME 5;

Limiting Account Inactivity: Example

The following statement modifies the profile `app_user2`
`INACTIVE_ACCOUNT_TIME` to 30 consecutive days:

    
    
    ALTER PROFILE app_user2 LIMIT
      INACTIVE_ACCOUNT_TIME 30;

If the account has already been inactive for a certain number of days, then
those days count toward the new 30 day limit.

Limiting Concurrent Sessions: Example

This statement defines a new limit of 5 concurrent sessions for the `app_user`
profile:

    
    
    ALTER PROFILE app_user LIMIT SESSIONS_PER_USER 5; 
    

If the `app_user` profile does not currently define a limit for
`SESSIONS_PER_USER`, then the preceding statement adds the limit of 5 to the
profile. If the profile already defines a limit, then the preceding statement
redefines it to 5. Any user assigned the `app_user` profile is subsequently
limited to 5 concurrent sessions.

Removing Profile Limits: Example

This statement removes the `IDLE_TIME `limit from the `app_user` profile:

    
    
    ALTER PROFILE app_user LIMIT IDLE_TIME DEFAULT;
    

Any user assigned the `app_user` profile is subject in their subsequent
sessions to the `IDLE_TIME` limit defined in the `DEFAULT` profile.

Limiting Profile Idle Time: Example

This statement defines a limit of 2 minutes of idle time for the `DEFAULT`
profile:

    
    
    ALTER PROFILE default LIMIT IDLE_TIME  2; 
    

This `IDLE_TIME` limit applies to these users:

  * Users who are not explicitly assigned any profile 

  * Users who are explicitly assigned a profile that does not define an `IDLE_TIME` limit 

This statement defines unlimited idle time for the `app_user2` profile:

    
    
    ALTER PROFILE app_user2 LIMIT IDLE_TIME UNLIMITED; 
    

Any user assigned the `app_user2` profile is subsequently permitted unlimited
idle time.

Enable Gradual Password Rollover: Example

This statement sets the password rollover time to 2 days in the profile
`usr_prof`:

    
    
    ALTER PROFILE usr_prof LIMIT PASSWORD_ROLLOVER_TIME 2 ;


[← Previous](ALTER-PROCEDURE.md)

[Next →](alter-property-graph.md)
