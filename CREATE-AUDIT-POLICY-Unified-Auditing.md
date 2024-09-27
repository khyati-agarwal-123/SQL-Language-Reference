[Previous](CREATE-ATTRIBUTE-DIMENSION.md) [Next](CREATE-CLUSTER.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: COMMIT to CREATE JAVA](SQL-Statements-COMMIT-to-CREATE-JAVA.md)
  3. CREATE AUDIT POLICY (Unified Auditing)

## CREATE AUDIT POLICY (Unified Auditing)

This section describes the `CREATE` `AUDIT` `POLICY` statement for unified
auditing. This type of auditing is new beginning with Oracle Database 12c and
provides a full set of enhanced auditing features. Refer to [Oracle Database
Security Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DBSEG630) for more information on unified auditing.

Purpose

Use the `CREATE` `AUDIT` `POLICY` statement to create a unified audit policy.

See Also:

  * [ALTER AUDIT POLICY (Unified Auditing)](ALTER-AUDIT-POLICY-Unified-Auditing.md#GUID-CC41B5C2-09F4-40BC-B7FD-3B4C0A3F5437)

  * [DROP AUDIT POLICY (Unified Auditing)](DROP-AUDIT-POLICY-Unified-Auditing.md#GUID-811D3F84-744E-47A1-B69D-C9D2FA4A0844)

  * [AUDIT (Unified Auditing)](AUDIT-Unified-Auditing.md#GUID-B24D6874-4053-4E66-8238-6CD0C87E9DCA)

  * [NOAUDIT (Unified Auditing)](NOAUDIT-Unified-Auditing.md#GUID-EB92BE04-B09C-493F-952E-9629E739900E)

Prerequisites

You must have the `AUDIT` `SYSTEM` system privilege or the `AUDIT_ADMIN` role.

To specify the `CONTAINER` clause, you must be connected to a multitenant
container database (CDB). To create a common unified audit policy, you must
have the commonly granted `AUDIT` `SYSTEM` privilege or the `AUDIT_ADMIN`
common role. To create a local unified audit policy, you must have the
commonly granted `AUDIT` `SYSTEM` privilege or the `AUDIT_ADMIN` common role,
or you must have the locally granted `AUDIT` `SYSTEM` privilege or the
`AUDIT_ADMIN` local role in the container to which you are connected.

Syntax

create_audit_policy::=

![Description of create_audit_policy.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_audit_policy.gif)  
[Description of the illustration
create_audit_policy.eps](img_text/create_audit_policy.md)

Note:

You must specify at least one of the clauses `privilege_audit_clause`,
`action_audit_clause`, or `role_audit_clause`.

([privilege_audit_clause::=](CREATE-AUDIT-POLICY-Unified-
Auditing.md#GUID-8D6961FB-2E50-46F5-81F7-9AEA314FC693__BGEDDIIC),
[action_audit_clause::=](CREATE-AUDIT-POLICY-Unified-
Auditing.md#GUID-8D6961FB-2E50-46F5-81F7-9AEA314FC693__BGEFFEGE),
[role_audit_clause::=](CREATE-AUDIT-POLICY-Unified-
Auditing.md#GUID-8D6961FB-2E50-46F5-81F7-9AEA314FC693__BGEEIAEG))

privilege_audit_clause::=

![Description of privilege_audit_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/privilege_audit_clause.gif)  
[Description of the illustration
privilege_audit_clause.eps](img_text/privilege_audit_clause.md)

action_audit_clause::=

![Description of action_audit_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/action_audit_clause.gif)  
[Description of the illustration
action_audit_clause.eps](img_text/action_audit_clause.md)

Note:

You can specify only the `standard_actions` clause, only the
`component_actions` clause, or both clauses in either order, but you can
specify each clause at most once.

standard_actions::=

![Description of standard_actions.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/standard_actions.gif)  
[Description of the illustration
standard_actions.eps](img_text/standard_actions.md)

component_actions::=

![Description of component_actions.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/component_actions.gif)  
[Description of the illustration
component_actions.eps](img_text/component_actions.md)

role_audit_clause::=

![Description of role_audit_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/role_audit_clause.gif)  
[Description of the illustration
role_audit_clause.eps](img_text/role_audit_clause.md)

Semantics

policy

Specify the name of the unified audit policy to be created. The name of the
policy must begin with the value of the `COMMON_USER_PREFIX` initialization
parameter. The default value of the `COMMON_USER_PREFIX` parameter is `c##`.

The length of the audit policy name cannot exceed 128 bytes and must contain
ASCII characters only.

These rules apply for application common audit policies as well. In this case,
the value of the `COMMON_USER_PREFIX` is fetched from the application root.
The default value in application root is an empty string.

The name must also satisfy the requirements listed in "[Database Object Naming
Rules](Database-Object-Names-and-
Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)".

You can find the names of all unified audit policies by querying the
`AUDIT_UNIFIED_POLICIES` view.

See Also:

[Oracle Database Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN29157) for more information on the
`AUDIT_UNIFIED_POLICIES` view

privilege_audit_clause

Use this clause to audit one or more system privileges. For
`system_privilege`, specify a valid system privilege. To view all valid system
privileges, query the `NAME` column of the `SYSTEM_PRIVILEGE_MAP` view.

Only those SQL statements are audited, that successfully use system
privileges. If a statement does not make use of a system privilege, it does
not get audited with the `privilege_audit_clause`.

Restriction on Auditing System Privileges

You cannot audit the following system privileges: `INHERIT` `ANY`
`PRIVILEGES`, `SYSASM`, `SYSBACKUP`, `SYSDBA`, `SYSDG`, `SYSKM`, `SYSRAC`, and
`SYSOPER`.

action_audit_clause

Use this clause to specify one or more actions to be audited. Use the
`standard_actions` clause to audit actions on standard RDBMS objects and to
audit standard RDBMS system actions for the database. Use the
`component_actions` clause to audit actions for components.

standard_actions

Use this clause to audit actions on standard RDBMS objects and to audit
standard RDBMS system actions for the database.

You can also create unified audit policies to audit individual columns in
tables and views. For examples on auditing columns see [Examples](CREATE-
AUDIT-POLICY-Unified-
Auditing.md#GUID-8D6961FB-2E50-46F5-81F7-9AEA314FC693__GUID-58013E01-AFF7-41D4-8E0E-4DB096112C64)

Note that column level audit policies generate audit records whenever the
column is accessed.

object_action ON

Use this clause to audit an action on the specified object. For
`object_action`, specify the action to be audited. [Table 13-1](CREATE-AUDIT-
POLICY-Unified-
Auditing.md#GUID-8D6961FB-2E50-46F5-81F7-9AEA314FC693__BGEGGCBI "Column 1
lists types of objects. Column 2 lists the valid actions for each type of
object.") lists the actions that can be audited on each type of object.

ALL ON

Use this clause to audit all actions on the specified object. All of the
actions listed in [Table 13-1](CREATE-AUDIT-POLICY-Unified-
Auditing.md#GUID-8D6961FB-2E50-46F5-81F7-9AEA314FC693__BGEGGCBI "Column 1
lists types of objects. Column 2 lists the valid actions for each type of
object.") for the type of object that you specify in the `ON` clause will be
audited.

ON Clause

Use the `ON` clause to specify the object to be audited. Directories and data
mining models are identified separately because they reside in separate
namespaces. To audit actions on a directory, specify `ON` `DIRECTORY`
`directory_name`. To audit actions on a data mining model, specify `ON`
`MINING` `MODEL` `object_name`. To audit actions on the other types of objects
listed in [Table 13-1](CREATE-AUDIT-POLICY-Unified-
Auditing.md#GUID-8D6961FB-2E50-46F5-81F7-9AEA314FC693__BGEGGCBI "Column 1
lists types of objects. Column 2 lists the valid actions for each type of
object."), specify `ON` `object_name`. If you do not qualify `object_name`
with `schema`, then the database assumes the object is in your own schema.

Table 13-1 Unified Auditing Objects and Actions

Type of Object | Actions  
---|---  
Directory |  `AUDIT`, `GRANT`, `READ`  
Function |  `AUDIT`, `EXECUTE` (Notes 1 and 2), `GRANT`  
Java Schema Objects (Source, Class, Resource) |  `AUDIT`, `EXECUTE`, `GRANT`  
Library |  `EXECUTE`, `GRANT`  
Materialized Views |  `ALTER`, `AUDIT`, `COMMENT`, `DELETE`, `INDEX`, `INSERT`, `LOCK`, `SELECT`, `UPDATE`  
Mining Model |  `AUDIT`, `COMMENT`, `GRANT`, `RENAME`, `SELECT`  
Object Type |  `ALTER`, `AUDIT`, `GRANT`  
Package |  `AUDIT`, `EXECUTE`, `GRANT`  
Procedure |  `AUDIT`, `EXECUTE` (Notes 1 and 2), `GRANT`  
Sequence |  `ALTER`, `AUDIT`, `GRANT`, `SELECT`  
Table |  `ALTER`, `AUDIT`, `COMMENT`, `DELETE`, `FLASHBACK`, `GRANT`, `INDEX`, `INSERT`, `LOCK`, `RENAME`, `SELECT`, `UPDATE`, `TRUNCATE`  
View |  `AUDIT`, `DELETE`, `FLASHBACK`, `GRANT`, `INSERT`, `LOCK`, `RENAME`, `SELECT`, `UPDATE`  
  
Note 1: When you audit the `EXECUTE` operation on a PL/SQL stored procedure or
stored function, the database considers only its ability to find the procedure
or function and authorize its execution when determining the success or
failure of the operation for the purposes of auditing. Therefore, if you
specify the `WHENEVER` `NOT` `SUCCESSFUL` clause, then only invalid object
errors, non-existent object errors, and authorization failures are audited;
errors encountered during the execution of the procedure or function are not
audited. If you specify the `WHENEVER` `SUCCESSFUL` clause, then all
executions that are not blocked by invalid object errors, non-existent object
errors, or authorization failures are audited, regardless of whether errors
are encountered during execution.

Note 2: To audit the failure of a recursive SQL operation inside a PL/SQL
stored procedure or stored function, configure auditing for the SQL operation.

Note 3: The auditing of `EXECUTE` on a PL/SQL stored procedure, function, or
package in the database happens during the instantiation phase of the
procedure, function, or package.

Note 3: The auditing of the `GRANT` object audit option also audits the
`REVOKE` audit option.

system_action

Use this clause to audit a system action for the database. To view the valid
values for `system_action`, query the `NAME` column of the
`AUDITABLE_SYSTEM_ACTIONS` view where `COMPONENT` is '`Standard`'.

Example: Audit CHANGE PASSWORD in Unified Auditing

You can audit `CHANGE PASSWORD` system actions by configuring an audit policy
to audit password changes. After you configure the audit policy, you must
enable the audit policy.

Example: Create Audit Policy to Audit System Action Change Password

The following example creates an audit policy `mypolicy` to audit the action
`CHANGE PASSWORD`:

    
    
    CREATE AUDIT POLICY mypolicy ACTIONS CHANGE PASSWORD;
    –---------------------
    Audit policy created.
    

Example: Enable Audit Policy Configured to Audit Password Changes

The following statement enables the audit policy `mypolicy`:

    
    
    AUDIT POLICY mypolicy;

The audit policy `mypolicy` will now audit `CHANGE PASSWORD` actions for both
successful and unsuccessful changes of password.

Example: Change Password

A user `hr_usr` with password `hr_pwd` can connect to PDB `hr_pdb` and change
the password as follows:

    
    
    CONNECT hr_usr/hr_pwd@hr_pdb;
    PASSWORD 
    Changing password for hr_usr
    Old password: 
    New password:
    Retype new password:
    Password changed.

In the SQL*Plus example above, the command `PASSWORD` run by user `hr_usr`
initiates a `CHANGE PASSWORD` action that generates an audit record.

Example: Check Audit Trail for Password Changes

You can view the record by by querying the `UNIFIED_AUDIT_TRAIL` as follows:

    
    
    SELECT ACTION_NAME, UNIFIED_AUDIT_POLICIES, OBJECT_NAME FROM UNIFIED_AUDIT_TRAIL;
    
    ACTION_NAME
    ----------------------------------------------------------------
    UNIFIED_AUDIT_POLICIES
    ----------------------------------------------------------------
    OBJECT_NAME
    ----------------------------------------------------------------
    CHANGE PASSWORD
    MYPOLICY
    HR_USR
    

Note that the audit policy `mypolicy` will not capture password changes via
the `ALTER USER` statement.

ALL

Use this clause to audit all system actions for the database.

component_actions

Use this clause to audit actions for the following components: Oracle Data
Pump, Oracle SQL*Loader Direct Path Load, Oracle Label Security, Oracle
Database Real Application Security, Oracle Database Vault, and the
transmission protocol.

DATAPUMP

Use this clause to audit actions for Oracle Data Pump. For `component_action`,
specify the action to be audited. To view the valid actions for Oracle Data
Pump, query the `NAME` column of the `AUDITABLE_SYSTEM_ACTIONS` view where
`COMPONENT` is `Datapump`. For example:

    
    
    SELECT name FROM auditable_system_actions WHERE component = 'Datapump';
    

Refer to [Oracle Database Security
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DBSEG928) for complete information on auditing Oracle
Data Pump.

DIRECT_LOAD

Use this clause to audit actions for Oracle SQL*Loader Direct Path Load. For
`component_action`, specify the action to be audited. To view the valid
actions for Oracle SQL*Loader Direct Path Load, query the `NAME` column of the
`AUDITABLE_SYSTEM_ACTIONS` view where `COMPONENT` is `Direct` `path` `API`.
For example:

    
    
    SELECT name FROM auditable_system_actions WHERE component = 'Direct path API';
    

Refer to [Oracle Database Security
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DBSEG120) for complete information on auditing Oracle
SQL*Loader Direct Path Load.

OLS

Use this clause to audit actions for Oracle Label Security. For
`component_action`, specify the action to be audited. To view the valid
actions for Oracle Label Security, query the `NAME` column of the
`AUDITABLE_SYSTEM_ACTIONS` view where `COMPONENT` is `Label` `Security`. For
example:

    
    
    SELECT name FROM auditable_system_actions WHERE component = 'Label Security';
    

Refer to [Oracle Database Security
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DBSEG454) for complete information on auditing Oracle
Label Security.

XS

Use this clause to audit actions for Oracle Database Real Application
Security. For `component_action`, specify the action to be audited. To view
the valid actions for Oracle Database Real Application Security, query the
`NAME` column of the `AUDITABLE_SYSTEM_ACTIONS` view where `COMPONENT` is
`XS`. For example:

    
    
    SELECT name FROM auditable_system_actions WHERE component = 'XS';
    

Refer to [Oracle Database Security
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DBSEG367) for complete information on auditing Oracle
Database Real Application Security.

DV

Use this clause to audit actions for Oracle Database Vault. For
`component_action`, specify the action to be audited. To view the valid
actions for Oracle Database Vault, query the `NAME` column of the
`AUDITABLE_SYSTEM_ACTIONS` view where `COMPONENT` is `Database` `Vault`. For
example:

    
    
    SELECT name FROM auditable_system_actions WHERE component = 'Database Vault';
    

For `object_name`, specify the name of the Database Vault object to be
audited.

Refer to [Oracle Database Security
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DBSEG419) for complete information on auditing Oracle
Database Vault.

PROTOCOL

Use the `PROTOCOL `component to audit FTP and HTTP messages.

Example 1: Audit all HTTP Messages

    
    
    CREATE AUDIT POLICY mypolicy ACTIONS COMPONENT = PROTOCOL HTTP
        AUDIT POLICY mypolicy

Example 2: Audit Failed FTP Messages

    
    
    CREATE AUDIT POLICY mypolicy ACTIONS COMPONENT = PROTOCOL FTP
        AUDIT POLICY mypolicy WHENEVER NOT SUCCESSFUL

Example 3: Audit HTTP Messages that had 401 AUTH Replies

    
    
    CREATE AUDIT POLICY mypolicy ACTIONS COMPONENT = PROTOCOL AUTHENTICATION
        AUDIT POLICY mypolicy

role_audit_clause

Use this clause to specify one or more roles to be audited. When you audit a
role, Oracle Database audits all system privileges that are granted directly
to the role. SQL statements that require the system privileges in order to
succeed are audited. For `role`, specify either a user-defined (local or
external) or predefined role. For a list of predefined roles, refer to [Oracle
Database Security Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DBSEG4414).

WHEN Clause

Use this clause to control when the unified audit policy is enforced.

audit_condition

Specify a condition that determines if the unified audit policy is enforced.
If `audit_condition` evaluates to `TRUE`, then the policy is enforced. If
`FALSE`, then the policy is not enforced.

The `audit_condition` can have a maximum length of 4000 characters. It can
contain expressions, as well as the following functions and conditions:

  * Numeric functions: `BITAND`, `CEIL`, `FLOOR`, `POWER`

  * Character functions returning character values: `CONCAT`, `LOWER`, `UPPER`

  * Character functions returning number values: `INSTR`, `LENGTH`

  * Environment and identifier functions: `SYS_CONTEXT`, `UID`

  * Comparison conditions: `=`, `!=`, `<>`, `<`, `>`, `<=`, `>=`

  * Logical conditions: `AND`, `OR`

  * Null conditions: `IS` `[NOT]` `NULL`

  * `[NOT] ``BETWEEN` condition 

  * `[NOT]` `IN` condition 

The `audit_condition` must be enclosed in single quotation marks. If the
`audit_condition` contains a single quotation mark, then specify two single
quotation marks instead. For example, to specify the following condition:

    
    
    SYS_CONTEXT('USERENV', 'CLIENT_IDENTIFIER') = 'myclient'
    

Specify the following for `'``audit_condition``'`:

    
    
    'SYS_CONTEXT(''USERENV'', ''CLIENT_IDENTIFIER'') = ''myclient'''

The `EVALUATE PER` clauses evaluate the audit condition per instance per
container. For example, if a condition is evaluated in one container, it will
be evaluated again in any other container even if the instance is same.

EVALUATE PER STATEMENT

Specify this clause to evaluate the `audit_condition` for each auditable
statement for each instance in the container. If the `audit_condition`
evaluates to `TRUE`, then the unified audit policy is enforced for the
statement. If `FALSE`, then the unified audit policy is not enforced for the
statement.

EVALUATE PER SESSION

Specify this clause to evaluate the `audit_condition` once during the session.
The `audit_condition` is evaluated for the first auditable statement that is
executed during the session. If the `audit_condition` evaluates to `TRUE`,
then the unified audit policy is enforced for all applicable statements for
the rest of the session. If `FALSE`, then the unified audit policy is not
enforced for all applicable statements for the rest of the session.

EVALUATE PER INSTANCE

Specify this clause to evaluate the `audit_condition` once during the lifetime
of the instance. The `audit_condition` is evaluated for the first auditable
statement that is executed during the instance lifetime. If the
`audit_condition` evaluates to `TRUE`, then the unified audit policy is
enforced for all applicable statements for the rest of the lifetime of the
instance. If `FALSE`, then the unified audit policy is not enforced for all
applicable statements for the rest of the lifetime of the instance.

ONLY TOPLEVEL

Specify the `ONLY TOPLEVEL` clause when you want to audit the SQL statements
issued directly by a user.

SQL statements that are run from within a PL/SQL procedure are not considered
top-level statements. You can audit top-level statements from all users,
including user `SYS`.

For more see [Database Security
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DBSEG-GUID-D9A133FD-728C-4231-8870-A91280563D28).

CONTAINER Clause

Use the `CONTAINER` clause to specify the scope of the unified audit policy.

  * Specify `CONTAINER` `=` `ALL` to create a common unified audit policy. This type of policy is available to all pluggable databases (PDBs) in the CDB. The current container must be the root. If you specify the `ACTIONS` `object_action` `ON` or `ACTIONS` `ALL` `ON` clause, then you must specify a common object or an application common object. 

  * Specify `CONTAINER` `=` `CURRENT` to create a local unified audit policy in the current container. The current container can be the root or a PDB. 

If you omit this clause, then `CONTAINER` `=` `CURRENT` is the default.

Note:

You cannot alter the scope of a unified audit policy after it has been
created.

Examples

Auditing System Privileges: Example

The following statement creates unified audit policy `table_pol`, which audits
the system privileges `CREATE` `ANY` `TABLE` and `DROP` `ANY` `TABLE`:

    
    
    CREATE AUDIT POLICY table_pol
      PRIVILEGES CREATE ANY TABLE, DROP ANY TABLE;
    

The following statement verifies that `table_pol` now appears in the
`AUDIT_UNIFIED_POLICIES` view:

    
    
    SELECT *
      FROM audit_unified_policies
      WHERE policy_name = 'TABLE_POL';

Auditing Actions on Objects: Examples

The following statement creates unified audit policy `dml_pol`, which audits
`DELETE`, `INSERT`, and `UPDATE` actions on table `hr`.`employees`, and all
auditable actions on table `hr`.`departments`:

    
    
    CREATE AUDIT POLICY dml_pol
      ACTIONS DELETE on hr.employees,
              INSERT on hr.employees,
              UPDATE on hr.employees,
              ALL on hr.departments;
    

The following statement creates unified audit policy `read_dir_pol`, which
audits `READ` actions on directory `bfile_dir` (created in "[Creating a
Directory: Examples](CREATE-
DIRECTORY.md#GUID-8E9C569A-1B06-42C4-9586-0EF83437001A__I2092417)"):

    
    
    CREATE AUDIT POLICY read_dir_pol
      ACTIONS READ ON DIRECTORY bfile_dir;

Auditing System Actions: Examples

The following query displays the standard RDBMS system actions that can be
audited for the database:

    
    
    SELECT name FROM auditable_system_actions
      WHERE component = 'Standard'
      ORDER BY name;
    
    NAME
    ----
    ADMINISTER KEY MANAGEMENT
    ALL
    ALTER ASSEMBLY
    ALTER AUDIT POLICY
    ALTER CLUSTER
    ...
    

The following statement creates unified audit policy `security_pol`, which
audits the system action `ADMINISTER` `KEY` `MANAGEMENT`:

    
    
    CREATE AUDIT POLICY security_pol
      ACTIONS ADMINISTER KEY MANAGEMENT;
    

The following statement creates unified audit policy `dir_pol`, which audits
all read, write, and execute operations on any directory:

    
    
    CREATE AUDIT POLICY dir_pol
      ACTIONS READ DIRECTORY, WRITE DIRECTORY, EXECUTE DIRECTORY;

The following statement creates unified audit policy `all_actions_pol`, which
audits all standard RDBMS system actions for the database:

    
    
    CREATE AUDIT POLICY all_actions_pol
      ACTIONS ALL;

Auditing Component Actions: Example

The following query displays the actions that can be audited for Oracle Data
Pump:

    
    
    SELECT name FROM auditable_system_actions
      WHERE component = 'Datapump';
    
    NAME
    ----
    EXPORT
    IMPORT
    ALL
    

The following statement creates unified audit policy `dp_actions_pol`, which
audits `IMPORT` actions for Oracle Data Pump:

    
    
    CREATE AUDIT POLICY dp_actions_pol
      ACTIONS COMPONENT = datapump IMPORT;

Auditing Roles: Example

The following statement creates unified audit policy `java_pol`, which audits
the predefined roles `java_admin` and `java_deploy`:

    
    
    CREATE AUDIT POLICY java_pol
      ROLES java_admin, java_deploy;

Auditing System Privileges, Actions, and Roles: Example

The following statement creates unified audit policy `hr_admin_pol`, which
audits multiple system privileges, actions, and roles:

    
    
    CREATE AUDIT POLICY hr_admin_pol
      PRIVILEGES CREATE ANY TABLE, DROP ANY TABLE
      ACTIONS DELETE on hr.employees,
              INSERT on hr.employees,
              UPDATE on hr.employees,
              ALL on hr.departments,
              LOCK TABLE
      ROLES audit_admin, audit_viewer;

Controlling When a Unified Audit Policy is Enforced: Examples

The following statement creates unified audit policy `order_updates_pol`,
which audits `UPDATE` actions on table `oe`.`orders`. This policy is enforced
only when the auditable statement is issued by an external user. The audit
condition is checked once per session.

    
    
    CREATE AUDIT POLICY order_updates_pol
      ACTIONS UPDATE ON oe.orders
      WHEN 'SYS_CONTEXT(''USERENV'', ''IDENTIFICATION_TYPE'') = ''EXTERNAL'''
      EVALUATE PER SESSION;
    

The following statement creates unified audit policy `emp_updates_pol`, which
audits `DELETE`, `INSERT`, and `UPDATE` actions on table `hr`.`employees`.
This policy is enforced only when the auditable statement is issued by a user
who does not have a UID of 100, 105, or 107. The audit condition is checked
for each auditable statement.

    
    
    CREATE AUDIT POLICY emp_updates_pol
            ACTIONS DELETE on hr.employees,
              INSERT on hr.employees,
              UPDATE on hr.employees
            WHEN 'UID NOT IN (100, 105, 107)'
            EVALUATE PER STATEMENT;

Creating a Local Unified Audit Policy: Example

The following statement creates local unified audit policy `local_table_pol`,
which audits the system privileges `CREATE` `ANY` `TABLE` and `DROP` `ANY`
`TABLE` in the current container:

    
    
    CREATE AUDIT POLICY local_table_pol
           PRIVILEGES CREATE ANY TABLE, DROP ANY TABLE
           CONTAINER = CURRENT;

Creating a Common Unified Audit Policy: Example

The following statement creates common unified audit policy
`common_role1_pol`, which audits the common role `c##role1` (created in
`CREATE` `ROLE` "[Examples](CREATE-
ROLE.md#GUID-B2252DC5-5AE7-49B7-9048-98062993E450__I2066883)") across the
entire CDB:

    
    
    CREATE AUDIT POLICY c##common_role1_pol
          ROLES c##role1
          CONTAINER = ALL;

Creating an Audit Policy on Columns: Example

The audit policy `pol` generates an audit record when granting privileges on
the column `job` in the `emp` table.

    
    
    CREATE AUDIT POLICY pol ACTIONS GRANT(job) on scott.emp;

The audit policy `pol` generates an audit record when a new department number
is inserted into the `dept` table.

    
    
    CREATE AUDIT POLICY pol ACTIONS INSERT(deptno) on scott.dept;


[← Previous](CREATE-ATTRIBUTE-DIMENSION.md)

[Next →](CREATE-CLUSTER.md)
