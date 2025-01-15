##  DROP CONTEXT {#GUID-1C5C56A8-A3A3-421B-BEC5-C6ECCA0B60D0} 

Purpose 

Use the ` DROP ` ` CONTEXT ` statement to remove a context namespace from the database. 

Removing a context namespace does not invalidate any context under that namespace that has been set for a user session. However, the context will be invalid when the user next attempts to set that context. 

> **note:** See Also: 

[ CREATE CONTEXT ](CREATE-CONTEXT.md#GUID-FDF62812-A884-479C-9C1B-5BD6DDEFE7FA) and [ *Oracle Database Security Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DBSEG70071) for more information on contexts 

Prerequisites 

You must have the ` DROP ` ` ANY ` ` CONTEXT ` system privilege. 

Syntax 

*drop_context* ::= 

![Description of drop_context.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_context.gif)[ Description of the illustration drop_context.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/drop_context.md)

Semantics 

*namespace* 

Specify the name of the context namespace to drop. You cannot drop the built-in namespace ` USERENV ` . 

> **note:** See Also: 

[ SYS_CONTEXT ](SYS_CONTEXT.md#GUID-B9934A5D-D97B-4E51-B01B-80C76A5BD086) for information on the ` USERENV ` namespace 

Examples 

Dropping an Application Context: Example 

The following statement drops the context created in [ CREATE CONTEXT ](CREATE-CONTEXT.md#GUID-FDF62812-A884-479C-9C1B-5BD6DDEFE7FA) : 
    
    
    ```
    DROP CONTEXT hr_context;
    ```
