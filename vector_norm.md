[Previous](vector_embedding.md) [Next](vector_serialize.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. VECTOR_NORM

## VECTOR_NORM

Syntax

  

![Description of vector_norm.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vector_norm.gif)  
[Description of the illustration vector_norm.eps](img_text/vector_norm.md)

  

Purpose

`VECTOR_NORM` returns the Euclidean norm of a vector `(SQRT(SUM((xi-yi)2)))`
as a `BINARY_DOUBLE`.

This value is also called magnitude or size and represents the Euclidean
distance between the vector and the origin.

Parameters

`expr` must evaluate to a vector.

If `expr` is NULL, NULL is returned.

Example

    
    
    SELECT VECTOR_NORM( TO_VECTOR('[4, 3]', 2, FLOAT32) );
    
    VECTOR_NORM(TO_VECTOR('[4,3]',2,FLOAT32))
    ____________________________________________
    5.0

See Also:

  * [Vector Functions](Single-Row-Functions.md#GUID-C0C477F1-8210-4CA9-A5FA-0A340C409892)

  * [Vector Distance Metrics of the AI Vector Search User's Guide.](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=VECSE-GUID-DBC136C1-7C63-4B7F-902B-2289FF375560)


[← Previous](vector_embedding.md)

[Next →](vector_serialize.md)
