[Previous](CREATE-DATABASE.md) [Next](CREATE-DIMENSION.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: COMMIT to CREATE JAVA](SQL-Statements-COMMIT-to-CREATE-JAVA.md)
  3. CREATE DATABASE LINK 

## CREATE DATABASE LINK

Purpose

Use the `CREATE` `DATABASE` `LINK` statement to create a database link. A
database link is a schema object in one database that enables you to access
objects on another database. The other database need not be an Oracle Database
system. However, to access non-Oracle systems you must use Oracle
Heterogeneous Services.

After you have created a database link, you can use it in SQL statements to
refer to tables, views, and PL/SQL objects in the other database by appending
`@``dblink` to the table, view, or PL/SQL object name. You can query a table
or view in the other database with the `SELECT` statement. You can also access
remote tables and views using any `INSERT`, `UPDATE`, `DELETE`, or `LOCK`
`TABLE` statement.

See Also:

  * [Oracle Database Development Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADFNS00907) for information about accessing remote tables or views with PL/SQL functions, procedures, packages, and data types 

  * [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN029) for information on distributed database systems 

  * [Oracle Database Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN002) for descriptions of existing database links in the `ALL_DB_LINKS`, `DBA_DB_LINKS`, and `USER_DB_LINKS` data dictionary views and for information on monitoring the performance of existing links through the `V$DBLINK` dynamic performance view 

  * [ALTER DATABASE LINK](ALTER-DATABASE-LINK.md#GUID-0259D771-9D04-4D86-A94D-61B621A3918A) for information on altering a database link when the password of a connection or authentication user changes. 

  * [DROP DATABASE LINK](DROP-DATABASE-LINK.md#GUID-89856C55-29FB-4B52-84A9-E53B8D115864) for information on dropping existing database links 

  * [INSERT](INSERT.md#GUID-903F8043-0254-4EE9-ACC1-CB8AC0AF3423), [UPDATE](UPDATE.md#GUID-027A462D-379D-4E35-8611-410F3AC8FDA5), [DELETE](DELETE.md#GUID-156845A5-B626-412B-9F95-8869B988ABD7), and [LOCK TABLE](LOCK-TABLE.md#GUID-4C00C6D9-C5C5-46CC-AD33-A64001744A4C) for using links in DML operations 

Prerequisites

To create a private database link, you must have the `CREATE` `DATABASE`
`LINK` system privilege. To create a public database link, you must have the
`CREATE` `PUBLIC` `DATABASE` `LINK` system privilege. Also, you must have the
`CREATE` `SESSION` system privilege on the remote Oracle Database.

Oracle Net must be installed on both the local and remote Oracle Databases.

Syntax

create_database_link::=

![Description of create_database_link.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_database_link.gif)  
[Description of the illustration
create_database_link.eps](img_text/create_database_link.md)

([dblink::=](Syntax-for-Schema-Objects-and-Parts-in-SQL-
Statements.md#GUID-3B6E39A1-A538-4A8C-A314-932851A22777__BABGJDDB))

dblink_authentication::=

![Description of dblink_authentication.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/dblink_authentication.gif)  
[Description of the illustration
dblink_authentication.eps](img_text/dblink_authentication.md)

Semantics

SHARED

Specify `SHARED` to create a database link that can be shared by multiple
sessions using a single network connection from the source database to the
target database. In a shared server configuration, shared database links can
keep the number of connections into the remote database from becoming too
large. Shared links are typically also public database links. However, a
shared private database link can be useful when many clients access the same
local schema, and therefore use the same private database link.

In a shared database link, multiple sessions in the source database share the
same connection to the target database. Once a session is established on the
target database, that session is disassociated from the connection, to make
the connection available to another session on the source database. To prevent
an unauthorized session from attempting to connect through the database link,
when you specify `SHARED` you must also specify the `dblink_authentication`
clause for the users authorized to use the database link.

See Also:

[Oracle Database Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN029) for more information about shared database
links

PUBLIC

Specify `PUBLIC` to create a public database link visible to all users. If you
omit this clause, then the database link is private and is available only to
you.

The data accessible on the remote database depends on the identity the
database link uses when connecting to the remote database:

  * If you specify `CONNECT` `TO` `user` `IDENTIFIED` `BY` `password`, then the database link connects with the specified user and password. 

  * If you specify `CONNECT` `TO` `CURRENT_USER`, then the database link connects with the user in effect based on the scope in which the link is used. 

  * If you omit both of those clauses, then the database link connects to the remote database as the locally connected user.

See Also:

"[Defining a Public Database Link: Example](CREATE-DATABASE-
LINK.md#GUID-D966642A-B19E-449D-9968-1121AF06D793__I2133775)"

dblink

Specify the complete or partial name of the database link. If you specify only
the database name, then Oracle Database implicitly appends the database domain
of the local database.

Use only ASCII characters for `dblink`. Multibyte characters are not
supported. The database link name is case insensitive and is stored in
uppercase ASCII characters. If you specify the database name as a quoted
identifier, then the quotation marks are silently ignored.

If the value of the `GLOBAL_NAMES` initialization parameter is `TRUE`, then
the database link must have the same name as the database to which it
connects. If the value of `GLOBAL_NAMES` is `FALSE`, and if you have changed
the global name of the database, then you can specify the global name.

The maximum number of database links that can be open in one session or one
instance of an Oracle RAC configuration depends on the value of the
`OPEN_LINKS` and `OPEN_LINKS_PER_INSTANCE` initialization parameters.

Restriction on Creating Database Links

You cannot create a database link in another user's schema, and you cannot
qualify `dblink` with the name of a schema. Periods are permitted in names of
database links, so Oracle Database interprets the entire name, such as
`ralph.linktosales`, as the name of a database link in your schema rather than
as a database link named `linktosales` in the schema `ralph`.

See Also:

  * "[References to Objects in Remote Databases](Syntax-for-Schema-Objects-and-Parts-in-SQL-Statements.md#GUID-61D0B206-A5EA-473F-AD04-7067D6E3914C)" for guidelines for naming database links 

  * [Oracle Database Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=GUID-FD266F6F-D047-4EBB-8D96-B51B1DCA2D61) for information on the `GLOBAL_NAMES`, `OPEN_LINKS`, and `OPEN_LINKS_PER_INSTANCE` initialization parameters 

  * "[RENAME GLOBAL_NAME Clause](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2141769)" (an `ALTER` `DATABASE` clause) for information on changing the database global name 

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the database link does not exist, a new database link is created at the end of the statement.

  * If the database link exists, this is the database link you have at the end of the statement. A new one is not created because the older database link is detected.

Using `IF EXISTS` with `CREATE` results in `ORA-11543: Incorrect IF NOT EXISTS
clause for CREATE statement.`

CONNECT TO Clause

The `CONNECT` `TO` clause lets you specify the user and credentials, if any,
to be used to connect to the remote database.

CURRENT_USER Clause

Specify `CURRENT_USER` to create a current user database link. The current
user must be a global user with a valid account on the remote database.

If the database link is used directly rather than from within a stored object,
then the current user is the same as the connected user.

When executing a stored object (such as a procedure, view, or trigger) that
initiates a database link, `CURRENT_USER` is the name of the user that owns
the stored object, and not the name of the user that called the object. For
example, if the database link appears inside procedure `scott.p` (created by
`scott`), and user `jane` calls procedure `scott.p`, then the current user is
`scott`.

However, if the stored object is an invoker-rights function, procedure, or
package, then the invoker's authorization ID is used to connect as a remote
user. For example, if the privileged database link appears inside procedure
`scott.p` (an invoker-rights procedure created by `scott`), and user Jane
calls procedure `scott.p`, then `CURRENT_USER` is `jane` and the procedure
executes with Jane's privileges.

See Also:

  * [CREATE FUNCTION](CREATE-FUNCTION.md#GUID-156AEDAC-ADD0-4E46-AA56-6D1F7CA63306) for more information on invoker-rights functions 

  * "[Defining a CURRENT_USER Database Link: Example](CREATE-DATABASE-LINK.md#GUID-D966642A-B19E-449D-9968-1121AF06D793__I2143859)"

user IDENTIFIED BY password

Specify the user name and password used to connect to the remote database
using a fixed user database link. If you omit this clause, then the database
link uses the user name and password of each user who is connected to the
database. This is called a connected user database link.

You can set the password to a maximum length of 1024 bytes.

See Also:

"[Defining a Fixed-User Database Link: Example](CREATE-DATABASE-
LINK.md#GUID-D966642A-B19E-449D-9968-1121AF06D793__I2061718)"

dblink_authentication

You can specify this clause only if you are creating a shared database
linkâthat is, you have specified the `SHARED` clause. Specify the username
and password on the target instance. This clause authenticates the user to the
remote server and is required for security. The specified username and
password must be a valid username and password on the remote instance. The
username and password are used only for authentication. No other operations
are performed on behalf of this user.

CONNECT WITH Clause

Use `CONNECT WITH` to specify the credential object that stores the username
and password to connect to the remote database.

You can create, update, or drop the credential using the `DBMS_CREDENTIAL`
package.

You can use a credential object belonging to another user, if that user has
granted you execute privileges on the credential object.

USING 'connect string'

Specify the service name of a remote database. If you specify only the
database name, then Oracle Database implicitly appends the database domain to
the connect string to create a complete service name. Therefore, if the
database domain of the remote database is different from that of the current
database, then you must specify the complete service name.

See Also:

[Oracle Database Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN029) for information on specifying remote databases

Examples

The examples that follow assume two databases, one with the database name
`local` and the other with the database name `remote`. The examples use the
Oracle Database domain. Your database domain will be different.

Defining a Public Database Link: Example

The following statement defines a shared public database link named `remote`
that refers to the database specified by the service name `remote`:

    
    
    CREATE PUBLIC DATABASE LINK remote 
       USING 'remote'; 
    

This database link allows user `hr` on the `local` database to update a table
on the `remote` database (assuming `hr` has appropriate privileges):

    
    
    UPDATE employees@remote
       SET salary=salary*1.1
       WHERE last_name = 'Baer';

Defining a Fixed-User Database Link: Example

In the following statement, user `hr` on the `remote` database defines a
fixed-user database link named `local` to the `hr` schema on the `local`
database:

    
    
    CREATE DATABASE LINK local 
       CONNECT TO hr IDENTIFIED BY password
       USING 'local';
    

After this database link is created, `hr` can query tables in the schema `hr`
on the `local` database in this manner:

    
    
    SELECT * FROM employees@local;
    

User `hr` can also use DML statements to modify data on the `local` database:

    
    
    INSERT INTO employees@local
       (employee_id, last_name, email, hire_date, job_id)
       VALUES (999, 'Claus', 'sclaus@example.com', SYSDATE, 'SH_CLERK');
    
    UPDATE jobs@local SET min_salary = 3000
       WHERE job_id = 'SH_CLERK';
    
    DELETE FROM employees@local 
       WHERE employee_id = 999;
    

Using this fixed database link, user hr on the `remote` database can also
access tables owned by other users on the same database. This statement
assumes that user `hr` has the `READ` or `SELECT` privilege on the
`oe.customers` table. The statement connects to the user `hr` on the `local`
database and then queries the `oe`.`customers` table:

    
    
    SELECT * FROM oe.customers@local;

Defining a CURRENT_USER Database Link: Example

The following statement defines a current-user database link to the `remote`
database, using the entire service name as the link name:

    
    
    CREATE DATABASE LINK remote.us.example.com
       CONNECT TO CURRENT_USER
       USING 'remote';
    

The user who issues this statement must be a global user registered with the
LDAP directory service.

You can create a synonym to hide the fact that a particular table is on the
`remote` database. The following statement causes all future references to
`emp_table` to access the `employees` table owned by `hr` on the `remote`
database:

    
    
    CREATE SYNONYM emp_table 
       FOR oe.employees@remote.us.example.com;


[← Previous](CREATE-DATABASE.md)

[Next →](CREATE-DIMENSION.md)
