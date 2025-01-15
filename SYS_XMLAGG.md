##  SYS_XMLAGG {#GUID-BEDD241D-360A-46A2-AEBF-C8B70E465D75} 

Syntax 

![Description of sys_xmlagg.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/sys_xmlagg.gif)[ Description of the illustration sys_xmlagg.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/sys_xmlagg.md)

Purpose 

` SYS_XMLAgg ` aggregates all of the XML documents or fragments represented by *expr* and produces a single XML document. It adds a new enclosing element with a default name ` ROWSET ` . If you want to format the XML document differently, then specify *fmt* , which is an instance of the ` XMLFormat ` object. 

> **note:** See Also: 

[ SYS_XMLGEN ](SYS_XMLGEN.md#GUID-1AC25984-F4AB-468E-BF53-561275AD44E8) and  " [ XML Format Model ](Format-Models.md#GUID-C6EB69EF-74DB-4C10-A02E-210D31616552) "  for using the attributes of the ` XMLFormat ` type to format ` SYS_XMLAgg ` results 

Examples 

The following example uses the ` SYS_XMLGen ` function to generate an XML document for each row of the sample table ` employees ` where the employee's last name begins with the letter R, and then aggregates all of the rows into a single XML document in the default enclosing element ` ROWSET ` : 
    
    
    ```
    SELECT SYS_XMLAGG(SYS_XMLGEN(last_name)) XMLAGG
       FROM employees
       WHERE last_name LIKE 'R%'
       ORDER BY xmlagg;
    
    XMLAGG
    --------------------------------------------------------------------------------
    
    
    Rajs
    Raphaely
    Rogers
    Russell
    
    ```
