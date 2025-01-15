##  TO_BOOLEAN {#GUID-B4FA8F5F-DD2A-4BEA-946A-B3CA60509294} 

Syntax 

  


![Description of to_boolean.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_boolean.gif)[ Description of the illustration to_boolean.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/to_boolean.md)

  


Purpose 

Use ` TO_BOOLEAN ` to explicitly convert character value expressions or numeric value expressions to boolean values. 

If *expr* is a string, it must evaluate to the allowed string inputs. See [ Table 2-6 ](Data-Types.md#GUID-285FFCA8-390D-4FA9-9A51-47B84EF5F83A__TABLE_H3B_FXB_1VB) . 

*expr* can take one of the following types, or null: 

  * A character string of type ` CHAR ` , ` VARCHAR2 ` , ` NCHAR ` , ` NVARCHAR2 `

  * A numeric value of type ` NUMBER ` , ` BINARY_FLOAT ` , or ` BINARY_DOUBLE `

  * A boolean value of type ` BOOLEAN ` . 




Examples 
    
    
    ```
    SELECT TO_BOOLEAN(0), TO_BOOLEAN('true'), TO_BOOLEAN('no');
    ```

The output is: 
    
    
    ```
    
    TO_BOOLEAN( TO_BOOLEAN( TO_BOOLEAN(
    ----------- ----------- -----------
    FALSE       TRUE        FALSE
    
    ```
    
    
    ```
    SELECT TO_BOOLEAN(1) FROM DUAL;
    ```

The output is: 
    
    
    ```
    
    TO_BOOLEAN( 
    ----------- 
    TRUE      
    ```

> **note:** See Also: 

  * *CAST* for conversion rules. 

  * *Boolean Data Type* for more details on the built-in boolean data type. 



