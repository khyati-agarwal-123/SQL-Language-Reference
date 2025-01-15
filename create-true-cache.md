##  CREATE TRUE CACHE {#GUID-9CDFE592-D927-427F-A997-B9A50B646A56} 

Purpose 

Use ` CREATE TRUE CACHE ` to internally create and initialize the run-time management files required for True Cache, and also open True Cache for service. The set of run-time management files for True Cache operation include controlfile, ` SPFILE ` and tempfiles. 

Prerequisites 

  * You must set the initialization parameter ` TRUE_CACHE ` to ` TRUE ` to be in a True Cache environment. 

  * You must start the database in ` NOMOUNT ` mode. 




> **note:** See Also: 

*True Cache User's Guide* 

Syntax 

  


![Description of create_true_cache.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_true_cache.gif)[ Description of the illustration create_true_cache.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/create_true_cache.md)

  


Semantics 

To drop True Cache use [ DROP DATABASE ](DROP-DATABASE.md#GUID-4FFC1AF5-538D-4882-8979-7A9957492A23) . 
