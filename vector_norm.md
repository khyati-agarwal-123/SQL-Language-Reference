[Previous](vector_embedding.html) [Next](vector_serialize.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)2. [Functions](Functions.html)
  3. VECTOR_NORM



## VECTOR_NORM

`VECTOR_NORM` returns the Euclidean norm of a vector `(SQRT(SUM((xi-yi)2)))` as a `BINARY_DOUBLE`. This value is also called magnitude or size and represents the Euclidean distance between the vector and the origin. 

Syntax

  


![Description of vector_norm.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vector_norm.gif)[Descriptionof the illustration vector_norm.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/vector_norm.md)

  


Parameters

`expr` must evaluate to a vector. 

If `expr` is NULL, NULL is returned. 

Example
    
    
    SELECT VECTOR_NORM( TO_VECTOR('[4, 3]', 2, FLOAT32) );
    
    VECTOR_NORM(TO_VECTOR('[4,3]',2,FLOAT32))
    -----------------------------------------
    5.0E+000

[← Previous](vector_embedding.md)

[Next →](vector_serialize.md)
