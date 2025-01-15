##  XMLDIFF {#GUID-B7746C15-27FD-4CAF-87EA-49C0DFA1E935} 

Syntax 

![Description of xmldiff.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/xmldiff.gif)[ Description of the illustration xmldiff.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/xmldiff.md)

Purpose 

The ` XMLDiff ` function is the SQL interface for the XmlDiff C API. This function compares two XML documents and captures the differences in XML conforming to an Xdiff schema. The diff document is returned as an XMLType document. 

  * For the first two arguments, specify the names of two XMLType documents. 

  * For the *integer* , specify a number representing the hashLevel for a C function XmlDiff. If you do not want hashing, set this argument to 0 or omit it entirely. If you do not want hashing, but you want to specify flags, then you must set this argument to 0. 

  * For *string* , specify the flags that control the behavior of the function. These flags are specified by one or more names separated by semicolon. The names are the same as the names of constants for XmlDiff function. 




> **note:** See Also: 

[ *Oracle XML Developer's Kit Programmer's Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADXDK2510) for more information on using this function, including examples, and [ *Oracle Database XML C API Reference* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=CAXML6192) for information on the XML APIs for C 

Examples 

The following example compares two XML documents and returns the difference as an XMLType document: 
    
    
    ```
    SELECT XMLDIFF(
    XMLTYPE('
    
       
            
                    
                            Chapter 1.
                    
            
            
                     
                            Chapter 2.
                    
            
       
    '),
    XMLTYPE('
    
       
            
                    
                            Chapter 1.
                    
            
            
       
    ')
    )
    FROM DUAL; 
    ```
