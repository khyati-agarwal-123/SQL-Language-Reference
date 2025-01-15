##  Distributed Queries {#GUID-DADE67A5-1C58-4132-9B2F-C14AE9B65508} 

The Oracle distributed database management system architecture lets you access data in remote databases using Oracle Net and an Oracle Database server. You can identify a remote table, view, or materialized view by appending @ *dblink* to the end of its name. The *dblink* must be a complete or partial name for a database link to the database containing the remote table, view, or materialized view. 

> **note:** See Also: 

[ References to Objects in Remote Databases ](Syntax-for-Schema-Objects-and-Parts-in-SQL-Statements.md#GUID-61D0B206-A5EA-473F-AD04-7067D6E3914C) for more information on referring to database links 

Restrictions on Distributed Queries 

Distributed queries are currently subject to the restriction that all tables locked by a ` FOR ` ` UPDATE ` clause and all tables with ` LONG ` columns selected by the query must be located on the same database. In addition, Oracle Database currently does not support distributed queries that select user-defined types or object ` REF ` data types on remote tables. 
