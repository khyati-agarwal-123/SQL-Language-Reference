[Previous](CREATE-TRIGGER.md) [Next](CREATE-TYPE.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: CREATE SEQUENCE to DROP CLUSTER](SQL-Statements-CREATE-SEQUENCE-to-DROP-CLUSTER.md)
  3. CREATE TRUE CACHE

## CREATE TRUE CACHE

Purpose

Use `CREATE TRUE CACHE` to internally create and initialize the run-time
management files required for True Cache, and also open True Cache for
service. The set of run-time management files for True Cache operation include
controlfile, `SPFILE` and tempfiles.

Prerequisites

  * You must set the initialization parameter `TRUE_CACHE` to `TRUE` to be in a True Cache environment. 

  * You must start the database in `NOMOUNT` mode. 

See Also:

[True Cache User's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ODBTC-GUID-0E7F95E0-37C1-44E6-BC38-7C71D3DF4677)

Syntax

  

![Description of create_true_cache.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_true_cache.gif)  
[Description of the illustration
create_true_cache.eps](img_text/create_true_cache.md)

  

Semantics

To drop True Cache use [DROP DATABASE](DROP-
DATABASE.md#GUID-4FFC1AF5-538D-4882-8979-7A9957492A23).


[← Previous](CREATE-TRIGGER.md)

[Next →](CREATE-TYPE.md)
