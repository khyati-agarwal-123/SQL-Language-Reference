##  ALTER LIBRARY {#GUID-BB90AF66-3B1F-46C4-9716-4578DE0AE1F3} 

Purpose 

The ` ALTER ` ` LIBRARY ` statement explicitly recompiles a library. Explicit recompilation eliminates the need for implicit run-time recompilation and prevents associated run-time compilation errors and performance overhead. 

> **note:** 

This statement does not change the declaration or definition of an existing library. To redeclare or redefine a library, use the  " [ CREATE LIBRARY ](CREATE-LIBRARY.md#GUID-F042ABC9-2BF5-4E65-9D52-216D6228B288) "  with the ` OR ` ` REPLACE ` clause. 

Prerequisites 

If the library is in the ` SYS ` schema, you must be connected as ` SYSDBA ` . Otherwise, the library must be in your own schema or you must have the ` ALTER ` ` ANY ` ` LIBRARY ` system privilege. 

Syntax 

*alter_library* ::= 

![Description of alter_library.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_library.gif)[ Description of the illustration alter_library.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/alter_library.md)( *library_compile_clause* : See [ *Oracle Database PL/SQL Language Reference* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=LNPLS1877) for the syntax of this clause.) 

Semantics 

IF EXISTS 

Specify ` IF EXISTS ` to alter an existing table. 

Specifying ` IF NOT EXISTS ` with ` ALTER VIEW ` results in ` ORA-11544: Incorrect IF EXISTS clause for ALTER/DROP statement ` . 

*schema* 

Specify the schema containing the library. If you omit *schema* , then Oracle Database assumes the procedure is in your own schema. 

*library_name* 

Specify the name of the library to be recompiled. 

*library_compile_clause* 

See [ *Oracle Database PL/SQL Language Reference* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=LNPLS1877) for the syntax and semantics of this clause and for complete information on creating and compiling libraries. 

EDITIONABLE | NONEDITIONABLE 

Use these clauses to specify whether the library becomes an editioned or noneditioned object if editioning is later enabled for the schema object type ` LIBRARY ` in *schema* . The default is ` EDITIONABLE ` . For information about altering editioned and noneditioned objects, see [ *Oracle Database Development Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADFNS1287) . 
