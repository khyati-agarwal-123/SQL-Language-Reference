[Previous](ALTER-LIBRARY.md) [Next](ALTER-MATERIALIZED-VIEW.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ALTER LIBRARY to ALTER SESSION](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
  3. ALTER LOCKDOWN PROFILE

## ALTER LOCKDOWN PROFILE

Purpose

Use the `ALTER` `LOCKDOWN` `PROFILE` statement to alter a PDB lockdown
profile. You can use PDB lockdown profiles in a multitenant environment to
restrict user operations in pluggable databases (PDBs).

Immediately after you create a lockdown profile with the `CREATE` `LOCKDOWN`
`PROFILE` statement, all user operations are enabled for the profile. You can
then use the `ALTER` `LOCKDOWN` `PROFILE` statement to disable certain user
operations for the profile. When a lockdown profile is applied to a CDB,
application container, or PDB, users cannot perform the operations that are
the disabled for the profile. If you later would like to reenable some of the
disabled user operations, you can use the `ALTER` `LOCKDOWN` `PROFILE`
statement to do so.

The `ALTER` `LOCKDOWN` `PROFILE` statement allows you to disable or enable:

  * User operations associated with certain database features (using the `lockdown_features` clause) 

  * User operations associated with certain database options (using the `lockdown_options` clause) 

  * The issuance of certain SQL statements (using the `lockdown_statements` clause) 

See Also:

  * [CREATE LOCKDOWN PROFILE](CREATE-LOCKDOWN-PROFILE.md#GUID-1CDEC3A3-F3F1-4279-9370-36AACF416E0A) and [DROP LOCKDOWN PROFILE](DROP-LOCKDOWN-PROFILE.md#GUID-62D428C1-5081-43CA-B45D-7FF1B81363E7)

  * [Oracle Database Security Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DBSEG-GUID-AB5E62DB-7E2A-4B5A-BA96-A2BD2DF15275) for more information on PDB lockdown profiles 

Prerequisites

  * You must issue the `ALTER` `LOCKDOWN` `PROFILE` statement from the CDB Root or Application Root. 

  * You must have the `ALTER` `LOCKDOWN` `PROFILE` system privilege in the container in which you issue the statement. 

Syntax

alter_lockdown_profile::=

![Description of alter_lockdown_profile.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_lockdown_profile.gif)  
[Description of the illustration
alter_lockdown_profile.eps](img_text/alter_lockdown_profile.md)

lockdown_features::=

![Description of lockdown_features.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lockdown_features.gif)  
[Description of the illustration
lockdown_features.eps](img_text/lockdown_features.md)

lockdown_options::=

![Description of lockdown_options.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lockdown_options.gif)  
[Description of the illustration
lockdown_options.eps](img_text/lockdown_options.md)

lockdown_statements::=

![Description of lockdown_statements.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lockdown_statements.gif)  
[Description of the illustration
lockdown_statements.eps](img_text/lockdown_statements.md)

statement_clauses::=

![Description of statement_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/statement_clauses.gif)  
[Description of the illustration
statement_clauses.eps](img_text/statement_clauses.md)

clause_options::=

![Description of clause_options.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/clause_options.gif)  
[Description of the illustration
clause_options.eps](img_text/clause_options.md)

option_values::=

![Description of option_values.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/option_values.gif)  
[Description of the illustration
option_values.eps](img_text/option_values.md)

Semantics

profile_name

Specify the name of the PDB lockdown profile to be altered.

You can find the names of existing PDB lockdown profiles by querying the
`DBA_LOCKDOWN_PROFILES` data dictionary view.

lockdown_features

This clause lets you disable or enable user operations associated with certain
database features.

  * Specify `DISABLE` to add a restriction for the specified features. Users will be restricted from performing these operations in any PDB to which the profile applies. 

  * Specify `ENABLE` to remove a restriction for the specified features. Users will be allowed to perform these operations in any PDB to which the profile applies. 

  * Use `feature` to specify the features whose operations you want to disable or enable. [Table 11-1](ALTER-LOCKDOWN-PROFILE.md#GUID-B4029154-54A8-4B78-97C3-9CED416F1C34__PDBLOCKDOWNPROFILEFEATURES-2908FAD9 "Column 1 lists the feature type. Column 2 lists the feature name. Column 3 describes the operations associated with the feature.") lists the features you can specify and describes the operations associated with each feature. The table also indicates a feature bundle for each feature. For `feature`, you can specify a feature bundle name to disable or enable user operations for all features in that bundle, or you can specify an individual feature name. You can specify feature bundle names and feature names in any combination of uppercase and lowercase letters. 

  * Use `ALL` to specify all features listed in the table. 

  * Use `ALL` `EXCEPT` to specify all features listed in the table except the specified features. 

If you omit this clause, then the default is `ENABLE` `ALL`.

Note:

  * The Oracle Text type `FILE_DATASTORE` is deprecated. Oracle recommends that you replace `FILE_DATASTORE` indexes with the `DIRECTORY_DATASTORE` index type for greater security as it enables file access to be based on directory objects. 

  * The Oracle Text type `URL_DATASTORE` is deprecated. Oracle recommeds that you replace `URL_DATASTORE` with `NETWORK_DATASTORE`, which uses ACLs to control access to specific servers. 

Table 11-1 PDB Lockdown Profile Features

Feature Bundle | Feature | Operations  
---|---|---  
`AWR_ACCESS` |  `AWR_ACCESS` |  The PDB taking manual and automatic Automatic Workload Repository (AWR) snapshots  
`COMMON_SCHEMA_ACCESS` |  `COMMON_USER_LOCAL_SCHEMA_ACCESS` |  A common user invoking an invokerâs rights code unit or accessing a `BEQUEATH` `CURRENT_USER` view owned by any local user in the PDB   
`COMMON_SCHEMA_ACCESS` |  `LOCAL_USER_COMMON_SCHEMA_ACCESS ` | 

  * A local user with an `ANY` system privilege (for example, `CREATE` `ANY` `TABLE`) creating or accessing objects in a common userâs schema for which the privilege applies. Note: Disabling the `LOCAL_USER_COMMON_SCHEMA_ACCESS ` feature does not prevent a local user with the `SYSDBA` privilege or specific object privileges from creating or accessing objects in a common userâs schema. Therefore, Oracle recommends against granting such privileges to local users. 
  * A local user with the `BECOME` `USER` system privilege becoming a common user 
  * A local user altering a common user by issuing an `ALTER` `USER` statement 
  * A local user using a common user for proxy connections

  
`COMMON_SCHEMA_ACCESS` |  `SECURITY_POLICIES` |  Creation of certain security policies by a local user on a common object, including:

  * Data Redaction
  * Fine Grained Auditing (FGA)
  * Real Application Security (RAS)
  * Virtual Private Database (VPD)

  
`CONNECTIONS` |  `COMMON_USER_CONNECT` |  A common user connecting to the PDB directly. If this feature is disabled, then in order to connect to the PDB, a common user must first connect to the CDB root and then switch to the desired PDB using the `ALTER` `SESSION` `SET` `CONTAINER` statement.   
`CONNECTIONS` |  `LOCAL_SYSOPER_RESTRICTED_MODE_CONNECT` |  A local user with the `SYSOPER` privilege connecting to a PDB that is open in `RESTRICTED` mode   
`CTX_LOGGING` |  `CTX_LOGGING` |  Use logging in Oracle Text PL/SQL procedures such as `CTX_OUTPUT.START_LOG` and `CTX_OUTPUT.START_QUERY_LOG`  
`JAVA` |  `JAVA` |  Java as a whole. If this feature is disabled, then all options and features of the database that depend on Java will be disabled.  
`JAVA_RUNTIME` |  `JAVA_RUNTIME` |  Operations through Java that require `java.lang.RuntimePermission`  
`NETWORK_ACCESS` | `AQ_PROTOCOLS` |  Using HTTP, SMTP, and OCI notification features.  
`NETWORK_ACCESS` | `CTX_PROTOCOLS` | 

  * Operations that access the Oracle Text datastore types `DIRECTORY_DATASTORE` and `NETWORK_DATASTORE`.  The type `DIRECTORY_DATASTORE` has an attribute called `DIRECTORY` which is the directory object whose data is to be indexed. The default value of this attribute is null.  The `DIRECTORY_DATASTORE` type replaces the `FILE_DATASTORE` type, which is deprecated.  The `NETWORK_DATASTORE` type replaces the `URL_DATASTORE` type, which is deprecated.  The type `NETWORK_DATASTORE` conforms to the standard database security model for providing URL access based on access control lists (ACLs), which support the HTTP and HTTPS protocols.  The `URL_DATASTORE` type did not support HTTPS. 
  * Printing tokens as part of CTX logging with events `EVENT_INDEX_PRINT_TOKEN` and `EVENT_OPT_PRINT_TOKEN`

  
`NETWORK_ACCESS` | `DBMS_DEBUG_JDWP` |  Using the `DBMS_DEBUG_JDWP` PL/SQL package   
`NETWORK_ACCESS` | `UTL_HTTP` |  Using the `UTL_HTTP` PL/SQL package   
`NETWORK_ACCESS` | `UTL_INADDR` |  Using the `UTL_INADDR` PL/SQL package   
`NETWORK_ACCESS` | `UTL_SMTP` |  Using the `UTL_SMTP` PL/SQL package   
`NETWORK_ACCESS` | `UTL_TCP` |  Using the `UTL_TCP` PL/SQL package   
`NETWORK_ACCESS` | `XDB_PROTOCOLS` |  Using HTTP, FTP, and other network protocols through XDB  
`OS_ACCESS` |  `DROP_TABLESPACE_KEEP_DATAFILES` |  Dropping a tablespace in the PDB without specifying the `INCLUDING` `CONTENTS` `AND` `DATAFILES` clause in `DROP` `TABLESPACE` statement   
`OS_ACCESS` |  `EXTERNAL_FILE_ACCESS` |  Using external files or directory objects in the PDB when `PATH_PREFIX` is not set for the PDB   
`OS_ACCESS` |  `EXTERNAL_PROCEDURES` |  Using external procedure agent `extproc` in the PDB   
`OS_ACCESS` |  `FILE_TRANSFER` |  Using the `DBMS_FILE_TRANSFER` package   
`OS_ACCESS` |  `JAVA_OS_ACCESS` |  Using `java.io.FilePermission` from Java   
`OS_ACCESS` |  `LOB_FILE_ACCESS` |  Using `BFILE` and `CFILE` data types   
`OS_ACCESS` |  `TRACE_VIEW_ACCESS` |  Using the following trace views:

  * `[G]V$DIAG_OPT_TRACE_RECORDS`
  * `[G]V$DIAG_SQL_TRACE_RECORDS`
  * `[G]V$DIAG_TRACE_FILE_CONTENTS`
  * `V$DIAG_SESS_OPT_TRACE_RECORDS`
  * `V$DIAG_SESS_SQL_TRACE_RECORDS`

  
`OS_ACCESS` |  `UTL_FILE` |  Using `UTL_FILE`. If this feature is disabled, then the database blocks use of the `UTL_FILE.FOPEN` function.   
  
lockdown_options

This clause lets you disable or enable user operations associate with certain
database options.

  * Specify `DISABLE` to disable user operations for the specified options. Users will be restricted from performing these operations in any PDB to which the profile applies. 

  * Specify `ENABLE` to enable user operations for the specified options. Users will be allowed to perform these operations in any PDB to which the profile applies. 

  * For `option`, you can specify the following database options in any combination of uppercase and lowercase letters: 

    * `DATABASE` `QUEUING` – Represents user operations associated with the Oracle Database Advanced Queuing option 

    * `PARTITIONING` – Represents user operations associated with the Oracle Partitioning option 

  * Use `ALL` to specify all options in the preceding list. 

  * Use `ALL` `EXCEPT` to specify all options in the preceding list except the specified options. 

If you omit this clause, then the default is `ENABLE` `OPTION` `ALL`.

lockdown_statements

This clause lets you disable or enable the issuance of certain SQL statements.

  * Specify `DISABLE` to disable the issuance of the specified SQL statements. Users will be restricted from issuing these statements in any PDB to which the profile applies. 

  * Specify `ENABLE` to enable the issuance of the specified SQL statements. Users will be allowed to issue these statements in any PDB to which the profile applies. 

  * For `SQL_statement`, you can specify the following statements in any combination of uppercase and lowercase letters: 

    * `ADMINISTER` `KEY MANAGEMENT`

    * `ALTER` `DATABASE`

    * `ALTER` `PLUGGABLE` `DATABASE`

    * `ALTER` `SESSION`

    * `ALTER` `SYSTEM`

    * `ALTER` `TABLE`

    * `ALTER` `INDEX`

    * `ALTER` `TABLESPACE`

    * `ALTER` `PROFILE`

    * `CREATE` `TABLE`

    * `CREATE` `INDEX`

    * `CREATE` `TABLESPACE`

    * `CREATE` `PROFILE`

    * `CREATE` `DATABASE LINK`

    * `DROP` `TABLE`

    * `DROP` `INDEX`

    * `DROP` `TABLESPACE`

    * `DROP` `PROFILE`

  * Use `ALL` to specify all statements in the preceding list. 

  * Use `ALL` `EXCEPT` to specify all statements in the preceding list except the specified statements. 

If you omit this clause, then the default is `ENABLE` `STATEMENT` `ALL`.

statement_clauses

This clause lets you disable or enable specific clauses of the specified SQL
statement.

  * Use `clause` to specify the SQL keywords that form the clause you want to disable or enable. You can specify a clause in any combination of uppercase and lowercase letters. 

  * Use `ALL` to specify all clauses for the SQL statement. 

  * Use `ALL` `EXCEPT` to specify all clauses for the SQL statement except the specified clauses. 

For `clause`, you must specify at least enough keywords to unambiguously
identify a single clause for the SQL statement. The following are some
examples of how to specify `clause` for the `ALTER` `SYSTEM` statement:

  * To specify the [archive_log_clause::=](ALTER-SYSTEM.md#GUID-2C638517-D73A-41CA-9D8E-A62D1A0B7ADB__I2282125), specify `ARCHIVE`. This is sufficient because no other `ALTER` `SYSTEM` clause begins with the keyword `ARCHIVE`. Alternatively, you can specify `ARCHIVE` `LOG` for semantic clarity, but the `LOG` keyword is unnecessary. 

  * To specify either of the [rolling_migration_clauses::=](ALTER-SYSTEM.md#GUID-2C638517-D73A-41CA-9D8E-A62D1A0B7ADB__BABEEJEG), you must specify `START` `ROLLING` `MIGRATION` or `STOP` `ROLLING` `MIGRATION` in order to distinguish these clauses from the similarly named [rolling_patch_clauses::=](ALTER-SYSTEM.md#GUID-2C638517-D73A-41CA-9D8E-A62D1A0B7ADB__CCHFHEDI) `START` `ROLLING` `PATCH` and `STOP` `ROLLING` `PATCH`. 

  * You cannot specify the single keyword `FLUSH`, because several `ALTER` `SYSTEM` clauses begin with this keyword. You must instead specify each clause separately, such as `FLUSH` `SHARED_POOL` or `FLUSH` `GLOBAL` `CONTEXT`. 

There is no need to specify optional keywords within a clause, because they
have no effect. For example:

  * The [archive_log_clause::=](ALTER-SYSTEM.md#GUID-2C638517-D73A-41CA-9D8E-A62D1A0B7ADB__I2282125) has an optional `INSTANCE` keyword. However, you cannot enable or disable only `ARCHIVE` `LOG` clauses that contain the `INSTANCE` keyword. Specifying `ARCHIVE` `LOG` `INSTANCE` is equivalent to specifying `ARCHIVE` or `ARCHIVE` `LOG`. 

There is no need to specify parameter values within a clause, because they
have no effect. For example:

  * The [shutdown_dispatcher_clause::=](ALTER-SYSTEM.md#GUID-2C638517-D73A-41CA-9D8E-A62D1A0B7ADB__I2282153) requires you to specify a `dispatcher_name`. However, you cannot enable or disable `SHUTDOWN` clauses that contain a specific dispatcher name. Specifying `SHUTDOWN` `dispatcher1` is equivalent to specifying `SHUTDOWN`. 

See Also:

[ALTER DATABASE](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986), [ALTER PLUGGABLE
DATABASE](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7), [ALTER
SESSION](ALTER-SESSION.md#GUID-27186B28-7EFC-4998-B1ED-2B905CC0211B), and
[ALTER SYSTEM](ALTER-SYSTEM.md#GUID-2C638517-D73A-41CA-9D8E-A62D1A0B7ADB)
for complete information on the clauses for these statements

clause_options

This clause is valid only when you specify one of the following for
`lockdown_statements` and `statement_clauses`:

    
    
    { DISABLE | ENABLE } STATEMENT = ('ALTER SESSION') CLAUSE = ('SET')
    { DISABLE | ENABLE } STATEMENT = ('ALTER SYSTEM') CLAUSE = ('SET')

This clause lets you disable or enable the setting or modification of specific
options with the `ALTER` `SESSION` `SET` or `ALTER` `SYSTEM` `SET` statements.

  * Use `clause_option` to specify the option you want to disable or enable. 

  * Use `clause_option_pattern` to specify a pattern that matches multiple options. Within the pattern, specify a percent sign (%) to match zero or more characters in an option name. For example, specifying `'QUERY_REWRITE_%'` is equivalent to specifying both the `QUERY_REWRITE_ENABLED` and `QUERY_REWRITE_INTEGRITY` options. 

  * You can specify `clause_option` and `clause_option_pattern` in any combination of uppercase and lowercase letters. 

  * Use `ALL` to specify all options. 

  * Use `ALL` `EXCEPT` to specify all options except the specified options. 

See Also:

The [alter_session_set_clause](ALTER-
SESSION.md#GUID-27186B28-7EFC-4998-B1ED-2B905CC0211B__ALTER_SESSION_SET_CLAUSE-4BFDA0EA)
clause of `ALTER` `SESSION` and the [alter_system_set_clause](ALTER-
SYSTEM.md#GUID-2C638517-D73A-41CA-9D8E-A62D1A0B7ADB__I2061284) clause of
`ALTER` `SYSTEM` for complete information on the options you can specify for
these statements

option_values

This clause is valid only when you specify one of the following for
`lockdown_statements`, `statement_clauses`, and `clause_options`:

    
    
    DISABLE STATEMENT = ('ALTER SESSION') CLAUSE = ('SET') OPTION = clause_option
    DISABLE STATEMENT = ('ALTER SYSTEM') CLAUSE = ('SET') OPTION = clause_option

This clause lets you specify a default value for an option when disabling the
setting of that option. For options that take numeric values, this clause also
lets you restrict users from setting an option to certain values.

  * The `VALUE` clause lets you specify a default `option_value` for `clause_option`, which will go into effect for any PDB to which the profile applies after you close and reopen the PDB. If `clause_option` accepts multiple default values, then you can specify more than one `option_value` in a comma-separated list. The purpose of using this clause is to simultaneously set a default value for an option and restrict users from setting or modifying the value. 

  * The `MINVALUE` clause lets you restricts users from setting the value of `clause_option` to a value less than `option_value`. You can specify this clause only for options that take a numeric value. 

  * The `MAXVALUE` clause lets you restricts users from setting the value of `clause_option` to a value greater than `option_value`. You can specify this clause only for options that take a numeric value. 

  * You can specify both the `MINVALUE` and `MAXVALUE` clauses together to restrict users from setting the value of `clause_options` to any value less than `MINVALUE` or greater than `MAXVALUE`. 

  * `MINVALUE` and `MAXVALUE` settings take effect immediately when the lockdown profile is assigned to a PDB; you need not close and reopen the PDB. 

See Also:

[Oracle Database Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN-GUID-FD266F6F-D047-4EBB-8D96-B51B1DCA2D61) for
complete information on the values allowed for the various options

USERS Clause

As a CDB administrator or an Application administrator you can use the `USERS`
clause to configure lockdown rules for a specific set of users.

The values for `USERS` in a `CDB$ROOT` lockdown profile are as follows:

  * `USERS = ALL` means that the lockdown rule applies to all users in the PDB. 

  * `USERS = COMMON` means that the lockdown rule applies only to CDB `COMMON` users in the PDB. 

  * `USERS = LOCAL` means that the lockdown rule applies only to local users in the PDB. Application common users are considered local users at the CDB level. 

The values for `USERS` in an Application `ROOT` lockdown profile are as
follows:

  * `USERS = ALL` means that the lockdown rule applies to all users in the PDB. 

  * `USERS = COMMON` means that the lockdown rule applies only to Application `COMMON` users in the PDB. 

  * `USERS = LOCAL` means that the lockdown rule applies only to local users in the PDB. 

Note that the Application lockdown profile rules should not affect CDB common
users.

  * `ALL` users means Application common users and local users in the PDB. 

  * `COMMON` users means Application common users in the PDB. 

Examples

The following statement creates PDB lockdown profile `hr_prof`:

    
    
    CREATE LOCKDOWN PROFILE hr_prof;

The remaining examples in this section alter `hr_prof`.

Disabling Features for PDB Lockdown Profiles: Examples

The following statement disables all features in the feature bundle
`NETWORK_ACCESS`:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      DISABLE FEATURE = ('NETWORK_ACCESS');

The following statement disables the `LOB_FILE_ACCESS` and `TRACE_VIEW ACCESS`
features:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      DISABLE FEATURE = ('LOB_FILE_ACCESS', 'TRACE_VIEW_ACCESS');

The following statement disables all features except the
`COMMON_USER_LOCAL_SCHEMA_ACCESS` and `LOCAL_USER_COMMON_SCHEMA_ACCESS`
features:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      DISABLE FEATURE ALL EXCEPT = ('COMMON_USER_LOCAL_SCHEMA_ACCESS', 'LOCAL_USER_COMMON_SCHEMA_ACCESS');

The following statement disables all features:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      DISABLE FEATURE ALL;

Enabling Features for PDB Lockdown Profiles: Examples

The following statement enables the `UTL_HTTP` and `UTL_SMTP` features, as
well as all features in the feature bundle `OS_ACCESS`:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      ENABLE FEATURE = ('UTL_HTTP', 'UTL_SMTP', 'OS_ACCESS');

The following statement enables all features except the `AQ_PROTOCOLS` and
`CTX_PROTOCOLS` features:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      ENABLE FEATURE ALL EXCEPT = ('AQ_PROTOCOLS', 'CTX_PROTOCOLS');

The following statement enables all features:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      ENABLE FEATURE ALL;

Disabling Options for PDB Lockdown Profiles: Examples

The following statement disables user operations associated with the Oracle
Database Advanced Queuing option:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      DISABLE OPTION = ('DATABASE QUEUING');

The following statement disables user operations associated with the Oracle
Partitioning option:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      DISABLE OPTION = ('PARTITIONING');

Enabling Options for PDB Lockdown Profiles: Examples

The following statement enables user operations associated with the Oracle
Database Advanced Queuing option:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      ENABLE OPTION = ('DATABASE QUEUING');

The following statement enables user operations associated both with the
Oracle Database Advanced Queuing option and the Oracle Partitioning option:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      ENABLE OPTION ALL;

Disabling SQL Statements for PBB Lockdown Profiles: Examples

The following statement disables the `ALTER` `DATABASE` statement:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      DISABLE STATEMENT = ('ALTER DATABASE');

The following statement disables the `ALTER` `SYSTEM` `SUSPEND` and `ALTER`
`SYSTEM` `RESUME` statements:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      DISABLE STATEMENT = ('ALTER SYSTEM')
              CLAUSE = ('SUSPEND', 'RESUME');

The following statement disables all clauses of the `ALTER` `PLUGGABLE`
`DATABASE` statement, except `DEFAULT` `TABLESPACE` and `DEFAULT` `TEMPORARY`
`TABLESPACE`:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      DISABLE STATEMENT = ('ALTER PLUGGABLE DATABASE')
              CLAUSE ALL EXCEPT = ('DEFAULT TABLESPACE', 'DEFAULT TEMPORARY TABLESPACE');

The following statement disables using the `ALTER` `SESSION` statement to set
or modify `COMMIT_WAIT` or `CURSOR_SHARING`:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      DISABLE STATEMENT = ('ALTER SESSION')
              CLAUSE = ('SET')
              OPTION = ('COMMIT_WAIT', 'CURSOR_SHARING');

The following statement disables using the `ALTER` `SYSTEM` statement to set
or modify the value of `PDB_FILE_NAME_CONVERT`. It also sets the default value
for `PDB_FILE_NAME_CONVERT` to `'cdb1_pdb0', 'cdb1_pdb1'`. This default value
will take effect the next time the PDB is closed and reopened.

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      DISABLE STATEMENT = ('ALTER SYSTEM')
              CLAUSE = ('SET')
              OPTION = ('PDB_FILE_NAME_CONVERT')
              VALUE = ('cdb1_pdb0', 'cdb1_pdb1');

The following statement disables using the `ALTER` `SYSTEM` statement to set
or modify the value of `CPU_COUNT` to a value less than `8`:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      DISABLE STATEMENT = ('ALTER SYSTEM')
              CLAUSE = ('SET')
              OPTION = ('CPU_COUNT')
              MINVALUE = '8';

The following statement disables using the `ALTER` `SYSTEM` statement to set
or modify the value of `CPU_COUNT` to a value greater than `2`:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      DISABLE STATEMENT = ('ALTER SYSTEM')
              CLAUSE = ('SET')
              OPTION = ('CPU_COUNT')
              MAXVALUE = '2';

The following statement disables using the `ALTER` `SYSTEM` statement to set
or modify the value of `CPU_COUNT` to a value less than `2` or greater than
`6`:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      DISABLE STATEMENT = ('ALTER SYSTEM')
              CLAUSE = ('SET')
              OPTION = ('CPU_COUNT')
              MINVALUE = '2'
              MAXVALUE = '6';

Enabling SQL Statements for PBB Lockdown Profiles: Examples

The following statement enables all statements except `ALTER` `DATABASE`:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      ENABLE STATEMENT ALL EXCEPT = ('ALTER DATABASE');

The following statement enables the `ALTER` `DATABASE` `MOUNT` and `ALTER`
`DATABASE` `OPEN` statements:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      ENABLE STATEMENT = ('ALTER DATABASE')
              CLAUSE = ('MOUNT', 'OPEN');

The following statement enables all clauses of the `ALTER` `PLUGGABLE`
`DATABASE` statement, except `DEFAULT` `TABLESPACE` and `DEFAULT` `TEMPORARY`
`TABLESPACE`:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      ENABLE STATEMENT = ('ALTER PLUGGABLE DATABASE')
             CLAUSE ALL EXCEPT = ('DEFAULT TABLESPACE', 'DEFAULT TEMPORARY TABLESPACE');

The following statement enables using the `ALTER` `SESSION` statement to set
or modify `COMMIT_WAIT` or `CURSOR_SHARING`:

    
    
    ALTER LOCKDOWN PROFILE hr_prof
      ENABLE STATEMENT = ('ALTER SESSION')
             CLAUSE = ('SET')
             OPTION = ('COMMIT_WAIT', 'CURSOR_SHARING');


[← Previous](ALTER-LIBRARY.md)

[Next →](ALTER-MATERIALIZED-VIEW.md)
