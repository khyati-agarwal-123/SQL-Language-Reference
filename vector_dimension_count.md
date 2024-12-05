[Previous](vector_dims.html) [Next](vector_dimension_format.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)
  2. [Functions](Functions.html)
  3. VECTOR_DIMENSION_COUNT



## VECTOR_DIMENSION_COUNT

`VECTOR_DIMENSION_COUNT` returns the number of dimensions of a vector as a `NUMBER`. 

Syntax

  


![Description of vector_dimension_count.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vector_dimension_count.gif)[Description of the illustration vector_dimension_count.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/vector_dimension_count.html)

  


Purpose

`VECTOR_DIMENSION_COUNT` is synonymous with [VECTOR_DIMS](vector_dims.html#GUID-010349D7-190D-430B-A798-ACC486E1036A "VECTOR_DIMS returns the number of dimensions of a vector as a NUMBER. VECTOR_DIMS is synonymous with VECTOR_DIMENSION_COUNT."). 

Parameters

`expr` must evaluate to a vector. 

If `expr` is NULL, NULL is returned. 

Example
    
    
    SELECT VECTOR_DIMENSION_COUNT( TO_VECTOR('[34.6, 77.8]', 2, FLOAT64) );
    
    VECTOR_DIMENSION_COUNT(TO_VECTOR('[34.6,77.8]',2,FLOAT64))
    ----------------------------------------------------------
    2                          
    

[← Previous](vector_dims.md)

[Next →](vector_dimension_format.md)
