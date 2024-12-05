[Previous](vector_dimension_count.html) [Next](vector_embedding.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)2. [Functions](Functions.html)
  3. VECTOR_DIMENSION_FORMAT



## VECTOR_DIMENSION_FORMAT

`VECTOR_DIMENSION_FORMAT` returns the storage format of the vector. It returns a `VARCHAR2`, which can be one of the following values: `INT8`, `FLOAT32`, `FLOAT64`, or `BINARY`. 

Syntax

  


![Description of vector_dimension_format.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vector_dimension_format.gif)[Descriptionof the illustration vector_dimension_format.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/vector_dimension_format.md)

  


Parameters

`expr` must evaluate to a vector. 

If `expr` is NULL, NULL is returned. 

Examples
    
    
    SELECT VECTOR_DIMENSION_FORMAT(TO_VECTOR('[34.6, 77.8]', 2, FLOAT64));
    
    VECTOR_DIMENSION_FORMAT(TO_VECTOR('[34.6,77.8]',2,
    --------------------------------------------------
    FLOAT64
    
    
    SELECT VECTOR_DIMENSION_FORMAT(TO_VECTOR('[34.6, 77.8, 9]', 3, FLOAT32));
    
    VECTOR_DIMENSION_FORMAT(TO_VECTOR('[34.6,77.8,9]',
    --------------------------------------------------
    FLOAT32
    
    
    SELECT VECTOR_DIMENSION_FORMAT(TO_VECTOR('[34.6, 77.8, 9.10]', 3, INT8));
    
    VECTOR_DIMENSION_FORMAT(TO_VECTOR('[34.6,77.8,9.10
    --------------------------------------------------
    INT8
    
    
    SELECT VECTOR_DIMENSION_FORMAT(TO_VECTOR('[206, 32]', 16, BINARY));
    
    VECTOR_DIMENSION_FORMAT(TO_VECTOR('[206,32]',16,BI
    --------------------------------------------------
    BINARY
    
    
    SELECT VECTOR_DIMENSION_FORMAT(TO_VECTOR('[34.6, 77.8, 9, 10]', 3, INT8));
    
    SELECT VECTOR_DIMENSION_FORMAT(TO_VECTOR('[34.6, 77.8, 9, 10]', 3, INT8))
                                   *
    ERROR at line 1:
    ORA-51803: Vector dimension count must match the dimension count specified in
    the column definition (expected 3 dimensions, specified 4 dimensions).

[← Previous](vector_dimension_count.md)

[Next →](vector_embedding.md)
