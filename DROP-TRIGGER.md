##  DROP TRIGGER {#GUID-724AC8BC-0428-43D3-8F11-4D4AD8DC2984} 

Purpose 

Triggers are defined using PL/SQL. Refer to [ *Oracle Database PL/SQL Language Reference* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=LNPLS99990) for complete information on creating, altering, and dropping triggers. 

Use the ` DROP ` ` TRIGGER ` statement to remove a database trigger from the database. 

> **note:** See Also: 

[ CREATE TRIGGER ](CREATE-TRIGGER.md#GUID-EE0DF3AA-7ADC-4171-B8E8-138BE9224E3B) and [ ALTER TRIGGER ](ALTER-TRIGGER.md#GUID-085BD628-2903-46A3-9850-C0D8ED7F2EEF)

Prerequisites 

The trigger must be in your own schema or you must have the ` DROP ` ` ANY ` ` TRIGGER ` system privilege. To drop a trigger on ` DATABASE ` in another user's schema, you must also have the ` ADMINISTER ` ` DATABASE ` ` TRIGGER ` system privilege. 

Syntax 

*drop_trigger* ::= 

![Description of drop_trigger.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_trigger.gif)[ Description of the illustration drop_trigger.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/drop_trigger.md)

Semantics 

IF EXISTS 

Specify ` IF EXISTS ` to drop an existing object. 

Specifying ` IF NOT EXISTS ` with ` DROP ` results in ` ORA-11544: Incorrect IF EXISTS clause for ALTER/DROP statement ` . 

*schema* 

Specify the schema containing the trigger. If you omit *schema* , then Oracle Database assumes the trigger is in your own schema. 

*trigger* 

Specify the name of the trigger to be dropped. Oracle Database removes it from the database and does not fire it again. 

Examples 

Dropping a Trigger: Example 

The following statement drops the ` salary_check ` trigger in the schema ` hr ` : 
    
    
    ```
    DROP TRIGGER hr.salary_check; 
    ```
