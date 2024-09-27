[Previous](ALTER-DATABASE-DICTIONARY.md) [Next](ALTER-DIMENSION.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ADMINISTER KEY MANAGEMENT to ALTER JAVA](SQL-Statements-ADMINISTER-KEY-MANAGEMENT-to-ALTER-JAVA.md)
  3. ALTER DATABASE LINK 

## ALTER DATABASE LINK

Purpose

Use the `ALTER` `DATABASE` `LINK` statement to modify a fixed-user database
link when the password of the connection or authentication user changes.

Note:

  * You cannot use this statement to change the connection or authentication user associated with the database link. To change `user`, you must re-create the database link. 

  * You cannot use this statement to change the password of a connection or authentication user. You must use the [ALTER USER](ALTER-USER.md#GUID-9FCD038D-8193-4241-85CD-2F4723B27D44) statement for this purpose, and then alter the database link with the `ALTER` `DATABASE` `LINK` statement. 

  * This statement is valid only for fixed-user database links, not for connected-user or current user database links. See [CREATE DATABASE LINK](CREATE-DATABASE-LINK.md#GUID-D966642A-B19E-449D-9968-1121AF06D793) for more information on these two types of database links. 

Prerequisites

To alter a private database link, you must have the `ALTER` `DATABASE` `LINK`
system privilege. To alter a public database link, you must have the `ALTER`
`PUBLIC` `DATABASE` `LINK` system privilege.

Syntax

alter_database_link::=

![Description of alter_database_link.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_database_link.gif)  
[Description of the illustration
alter_database_link.eps](img_text/alter_database_link.md)

dblink_authentication

![Description of dblink_authentication.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/dblink_authentication.gif)  
[Description of the illustration
dblink_authentication.eps](img_text/dblink_authentication.md)

Semantics

The `ALTER` `DATABASE` `LINK` statement is intended only to update fixed-user
database links with the current passwords of connection and authentication
users. Therefore, any clauses valid in a `CREATE` `DATABASE` `LINK` statement
that do not appear in the syntax diagram above are not valid in an `ALTER`
`DATABASE` `LINK` statement. The semantics of all of the clauses permitted in
this statement are the same as the semantics for those clauses in `CREATE`
`DATABASE` `LINK`. Refer to [CREATE DATABASE LINK](CREATE-DATABASE-
LINK.md#GUID-D966642A-B19E-449D-9968-1121AF06D793) for this information.

IF EXISTS

Specify `IF EXISTS` to alter an existing database link.

Specifying `IF NOT EXISTS` with `ALTER VIEW` results in `ORA-11544: Incorrect
IF EXISTS clause for ALTER/DROP statement`.

IDENTIFIED BY

You can set the password length to a maximum length of 1024 bytes.

Examples

The following statements show the valid variations of the `ALTER` `DATABASE`
`LINK` statement:

    
    
    ALTER DATABASE LINK private_link 
      CONNECT TO hr IDENTIFIED BY hr_new_password;
    
    ALTER PUBLIC DATABASE LINK public_link
      CONNECT TO scott IDENTIFIED BY scott_new_password;
    
    ALTER SHARED PUBLIC DATABASE LINK shared_pub_link
      CONNECT TO scott IDENTIFIED BY scott_new_password
      AUTHENTICATED BY hr IDENTIFIED BY hr_new_password;
    
    ALTER SHARED DATABASE LINK shared_pub_link
      CONNECT TO scott IDENTIFIED BY scott_new_password;
    


[← Previous](ALTER-DATABASE-DICTIONARY.md)

[Next →](ALTER-DIMENSION.md)
