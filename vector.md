[Previous](VARIANCE.html) [Next](vector_chunks.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)
  2. [Functions](Functions.html)
  3. VECTOR



## VECTOR

`VECTOR` is synonymous with `TO_VECTOR`. 

Syntax

  


![Description of vector_vecse.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vector_vecse.gif)[Description of the illustration vector_vecse.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/vector_vecse.html)

  


Purpose

See [TO_VECTOR](to_vector.html#GUID-2CCAB607-A28B-43F7-A71D-9800C0B9A380 "TO_VECTOR is a constructor that takes a string of type VARCHAR2, CLOB, BLOB, or JSON as input, converts it to a vector, and returns a vector as output. TO_VECTOR also takes another vector as input, adjusts its format, and returns the adjusted vector as output. TO_VECTOR is synonymous with VECTOR.") for semantics and examples. 

Note:

Applications using Oracle Client 23ai libraries or Thin mode drivers can insert vector data directly as a string or a `CLOB`. For example: 
    
    
    INSERT INTO vecTab VALUES ('[1.1, 2.9, 3.14]');

Examples
    
    
    SELECT VECTOR('[34.6, 77.8]');
    
    VECTOR('[34.6,77.8]')
    ---------------------------------------------------------
    [3.45999985E+001,7.78000031E+001]
    
    
    
    SELECT VECTOR('[34.6, 77.8]', 2, FLOAT32);
    
    VECTOR('[34.6,77.8]',2,FLOAT32)
    ---------------------------------------------------------
    [3.45999985E+001,7.78000031E+001]
    
    
    
    SELECT VECTOR('[34.6, 77.8, -89.34]', 3, FLOAT32);
    
    VECTOR('[34.6,77.8,-89.34]',3,FLOAT32)
    -----------------------------------------------------------
    [3.45999985E+001,7.78000031E+001,-8.93399963E+001]

[← Previous](VARIANCE.md)

[Next →](vector_chunks.md)
