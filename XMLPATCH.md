##  XMLPATCH {#GUID-C52DA494-2840-475B-871F-1EA071299894} 

Syntax 

![Description of xmlpatch.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/xmlpatch.gif)[ Description of the illustration xmlpatch.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/xmlpatch.md)

Purpose 

The ` XMLPatch ` function is the SQL interface for the XmlPatch C API. This function patches an XML document with the changes specified. A patched ` XMLType ` document is returned. 

  * For the first argument, specify the name of the input ` XMLType ` document. 

  * For the second argument, specify the XMLType document containing the changes to be applied to the first document. The changes should conform to the Xdiff XML schema. You can supply the XML output from the Oracle XML Developer's Kit Java method ` diff() ` . 




> **note:** See Also: 

[ *Oracle XML Developer's Kit Programmer's Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADXDK2520) for more information on using this function, including examples, and [ *Oracle Database XML C API Reference* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=CAXML6192) for information on the XML APIs for C 

Examples 

The following example patches an ` XMLType ` document with the changes specified in another ` XMLType ` and returns a patched ` XMLType ` document: 
    
    
    ```
    SELECT XMLPATCH(
    XMLTYPE('
    
       
            
                    
                            Chapter 1.
                    
            
            
                     
                            Chapter 2.
                    
            
       
    '),
    XMLTYPE('
    
      
      
    ')
    )
    FROM DUAL;
    ```
