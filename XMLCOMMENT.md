##  XMLCOMMENT {#GUID-AECB7BCC-C60F-4E0C-BD9A-E52D8F1599C4} 

Syntax 

![Description of xmlcomment.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/xmlcomment.gif)[ Description of the illustration xmlcomment.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/xmlcomment.md)

Purpose 

` XMLComment ` generates an XML comment using an evaluated result of *value_expr* . The *value_expr* must resolve to a string. It cannot contain two consecutive dashes (hyphens). The value returned by the function takes the following form: 
    
    
    ```
    
    
    ```

If *value_expr* resolves to null, then the function returns null. 

> **note:** See Also: 

[ *Oracle XML DB Developer's Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADXDB1620) for more information on this function 

Examples 

The following example uses the ` DUAL ` table to illustrate the ` XMLComment ` syntax: 
    
    
    ```
    SELECT XMLCOMMENT('OrderAnalysisComp imported, reconfigured, disassembled')
       AS "XMLCOMMENT" FROM DUAL;
     
    XMLCOMMENT
    --------------------------------------------------------------------------------
    
    ```
