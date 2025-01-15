##  ALTER HIERARCHY {#GUID-37A4E442-EE3A-4239-8228-F08A2F666D91} 

Purpose 

Use the ` ALTER ` ` HIERARCHY ` statement to rename or compile a hierarchy. For other alterations, use ` CREATE ` ` OR ` ` REPLACE ` ` HIERARCHY ` . 

Prerequisites 

To alter a hierarchy in your own schema, you must have the ` ALTER ` ` HIERARCHY ` system privilege. To alter a hierarchy in another user's schema, you must have the ` ALTER ` ` ANY ` ` HIERARCHY ` system privilege or have been granted ` ALTER ` directly on the hierarchy. 

Syntax 

*alter_hierarchy* ::= 

![Description of alter_hierarchy.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_hierarchy.gif)[ Description of the illustration alter_hierarchy.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/alter_hierarchy.md)

Semantics 

IF EXISTS 

Specify ` IF EXISTS ` to alter an existing table. 

Specifying ` IF NOT EXISTS ` with ` ALTER VIEW ` results in ` ORA-11544: Incorrect IF EXISTS clause for ALTER/DROP statement ` . 

*schema* 

Specify the schema in which the hierarchy exists. If you do not specify a schema, then Oracle Database looks for the hierarchy in your own schema. 

*hierarchy_name* 

Specify the name of the hierarchy. 

RENAME TO 

Specify ` RENAME ` ` TO ` to change the name of the hierarchy. 

COMPILE 

Specify ` COMPILE ` to compile the hierarchy. 

*new_hier_name* 

Specify a new name for the hierarchy. 

Example 

The following statement changes the name of a hierarchy: 
    
    
    ```
    ALTER HIERARCHY product_hier RENAME TO myproduct_hier;
    ```
