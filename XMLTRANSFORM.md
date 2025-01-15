##  XMLTRANSFORM {#GUID-3B74EED2-E79F-4333-8C0B-02989DF5EEAA} 

Syntax 

![Description of xmltransform.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/xmltransform.gif)[ Description of the illustration xmltransform.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/xmltransform.md)

Purpose 

` XMLTransform ` takes as arguments an ` XMLType ` instance and an XSL style sheet, which is itself a form of ` XMLType ` instance. It applies the style sheet to the instance and returns an ` XMLType ` . 

This function is useful for organizing data according to a style sheet as you are retrieving it from the database. 

> **note:** See Also: 

[ *Oracle XML DB Developer's Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADXDB0900) for more information on this function 

Examples 

The ` XMLTransform ` function requires the existence of an XSL style sheet. Here is an example of a very simple style sheet that alphabetizes elements within a node: 
    
    
    ```
    CREATE TABLE xsl_tab (col1 XMLTYPE);
    
    INSERT INTO xsl_tab VALUES (
       XMLTYPE.createxml(
       ' 
        
          
            
            
            
              
                
               
             
          
           
            
          
          '));
    
    1 row created.
    
    ```

The next example uses the ` xsl_tab ` XSL style sheet to alphabetize the elements in one ` warehouse_spec ` of the sample table ` oe.warehouses ` : 
    
    
    ```
    SELECT XMLTRANSFORM(w.warehouse_spec, x.col1).GetClobVal()
       FROM warehouses w, xsl_tab x
       WHERE w.warehouse_name = 'San Francisco';
    
    XMLTRANSFORM(W.WAREHOUSE_SPEC,X.COL1).GETCLOBVAL()
    --------------------------------------------------------------------------------
    
      50000
      Rented
      Side load
      1
      Lot
      N
      12 ft
      Y
    
    ```
