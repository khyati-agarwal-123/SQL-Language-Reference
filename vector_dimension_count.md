[Previous](vector_dims.md) [Next](vector_dimension_format.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. VECTOR_DIMENSION_COUNT

## VECTOR_DIMENSION_COUNT

Syntax

  

![Description of vector_dimension_count.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vector_dimension_count.gif)  
[Description of the illustration
vector_dimension_count.eps](img_text/vector_dimension_count.md)

  

Purpose

`VECTOR_DIMENSION_COUNT` returns the number of dimensions of a vector as a
`NUMBER`.

`VECTOR_DIMENSION_COUNT` is synonymous with
[VECTOR_DIMS](vector_dims.md#GUID-010349D7-190D-430B-A798-ACC486E1036A).

Parameters

`expr` must evaluate to a vector.

If `expr` is NULL, NULL is returned.

Example

    
    
    SELECT VECTOR_DIMENSION_COUNT( TO_VECTOR('[34.6, 77.8]', 2, FLOAT64) );
    VECTOR_DIMENSION_COUNT(TO_VECTOR('[34.6,77.8]',2,FLOAT64))
    ----------------------------------------------------------                           
    

See Also:

  * [Vector Functions](Single-Row-Functions.md#GUID-C0C477F1-8210-4CA9-A5FA-0A340C409892)

  * [Vector Distance Metrics of the AI Vector Search User's Guide.](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=VECSE-GUID-DBC136C1-7C63-4B7F-902B-2289FF375560)


[← Previous](vector_dims.md)

[Next →](vector_dimension_format.md)
