[Previous](ALTER-JAVA.html) [Next](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)
  2. [ SQL Statements: ADMINISTER KEY MANAGEMENT to ALTER JSON RELATIONAL DUALITY VIEW](SQL-Statements-ADMINISTER-KEY-MANAGEMENT-to-ALTER-JAVA.html)
  3. ALTER JSON RELATIONAL DUALITY VIEW



## ALTER JSON RELATIONAL DUALITY VIEW

Use `ALTER JSON RELATIONAL DUALITY VIEW` to alter various options for a duality view like logical replication. 

Prerequisites

You must have one of the following privileges to use this statement:

  * The view must be in your own schema

  * You must have the `ALTER ANY TABLE` system privilege 

  * You must have the `OGG_CAPTURE` role 




Syntax

  


![Description of alter_json_relational_duality_view.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_json_relational_duality_view.gif)[Description of the illustration alter_json_relational_duality_view.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/alter_json_relational_duality_view.html)

  


duality_view_replication_clause

  


![Description of duality_view_replication_clause.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/duality_view_replication_clause.gif)[Description of the illustration duality_view_replication_clause.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/duality_view_replication_clause.html)

  


Semantics

duality_view_replication_clause

Steps to Enable Duality View Replication 

  * You can enable logical replication for the duality view using `ALTER JSON RELATIONAL DUALITY VIEW ENABLE LOGICAL REPLICATION`. 

You can also enable logical replication with the command [CREATE JSON RELATIONAL DUALITY VIEW](create-json-relational-duality-view.html#GUID-64B579AD-BF97-4B27-BF22-94C1FB6FD6DF)

  * Minimal (or subset database replication) supplemental logging must be enabled at the database or container level using `ALTER PLUGGABLE DATABASE ADD SUPPLEMENTAL LOG DATA DDL`. 

  * Database compatible parameter must be 23.4 or higher 

  * Database parameter at the CDB level enable_goldengate_replication must be TRUE 




To disable logical replication on a duality view use `ALTER JSON RELATIONAL DUALITY VIEW DISABLE LOGICAL REPLICATION`

Note:

On a multi instance RAC database, you must run the `ALTER SYSTEM ENABLE RAC TWO_STAGE ROLLING UPDATES ALL` DDL, before you can enable or disable logical replication. 

After you run `ALTER SYSTEM ENABLE RAC TWO_STAGE ROLLING UPDATES ALL` you cannot perform an online downgrade (unpatch) of your RAC database to DBRU23.5 or lower. You must take a downtime. 

On a single instance database, you do not need to run `ALTER SYSTEM ENABLE RAC TWO_STAGE ROLLING UPDATES ALL`. 

[← Previous](ALTER-JAVA.md)

[Next →](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
