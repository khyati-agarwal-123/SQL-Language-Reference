[Previous](vector_dimension_count.md) [Next](vector_embedding.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. VECTOR_DIMENSION_FORMAT

## VECTOR_DIMENSION_FORMAT

Syntax

  

![Description of vector_dimension_format.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vector_dimension_format.gif)  
[Description of the illustration
vector_dimension_format.eps](img_text/vector_dimension_format.md)

  

Purpose

`VECTOR_DIMENSION_FORMAT` returns the storage format of the vector. It returns
a `VARCHAR2`, which can be one of the following values: `INT8`, `FLOAT32`, or
`FLOAT64`.

Parameters

`expr` must evaluate to a vector.

If `expr` is NULL, NULL is returned.

Examples

    
    
    SELECT VECTOR_DIMENSION_FORMAT(TO_VECTOR('[34.6, 77.8]', 2, FLOAT64));
    FLOAT64
    
    SELECT VECTOR_DIMENSION_FORMAT(TO_VECTOR('[34.6, 77.8, 9]', 3, FLOAT32));
    FLOAT32
    
    SELECT VECTOR_DIMENSION_FORMAT(TO_VECTOR('[34.6, 77.8, 9, 10]', 3, INT8));
    SELECT VECTOR_DIMENSION_FORMAT(TO_VECTOR('[34.6, 77.8, 9, 10]', 3, INT8))                           
                                                                            *
    ERROR at line 1:
    ORA-51803: Vector dimension count must match the dimension count specified inthe column definition (actual: 4, required: 3).
    
    SELECT VECTOR_DIMENSION_FORMAT(TO_VECTOR('[34.6, 77.8, 9.10]', 3, INT8));
    VECTOR_DIMENSION_FORMAT(TO_VECTOR('[34.6,77.8,9.10
    --------------------------------------------------
    INT8
    
    SELECT TO_VECTOR('[34.6, 77.8, 9.10]', 3, INT8);
    TO_VECTOR('[34.6,77.8,9.10]',3,INT8)
    ---------------------------------------------------
    [3.5E+001,7.8E+001,9.0E+000]
    

See Also:

  * [Vector Functions](Single-Row-Functions.md#GUID-C0C477F1-8210-4CA9-A5FA-0A340C409892)

  * [Vector Distance Metrics of the AI Vector Search User's Guide.](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=VECSE-GUID-DBC136C1-7C63-4B7F-902B-2289FF375560)


[← Previous](vector_dimension_count.md)

[Next →](vector_embedding.md)
