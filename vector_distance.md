[Previous](vector_chunks.md) [Next](vector_dims.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. VECTOR_DISTANCE

## VECTOR_DISTANCE

Syntax

  

![Description of vector_distance.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vector_distance.gif)  
[Description of the illustration
vector_distance.eps](img_text/vector_distance.md)

  

Purpose

`VECTOR_DISTANCE` is the main function that you can use to calculate the
distance between two vectors.

`VECTOR_DISTANCE` takes two vectors as parameters. You can optionally specify
a distance metric to calculate the distance. If you do not specify a distance
metric, then the default distance metric is Cosine distance.

You can optionally use the following shorthand vector distance functions:

  * `L1_DISTANCE`

  * `L2_DISTANCE`

  * `COSINE_DISTANCE`

  * `INNER_PRODUCT`

All the vector distance functions take two vectors as input and return the
distance between them as a `BINARY_DOUBLE`.

Note the following caveats, if you use `VECTOR_DISTANCE` to perform a
similarity search:

  * If you do not specify a distance metric, then the default distance metric `COSINE` is used for both exact and approximate (index-based) searches. 

  * If you specify a distance metric that conflicts with the distance metric specified in a vector index, then the distance metric that you specify is used to perform the exact search. 

  * If you specify a distance metric that matches the distance metric specified in a vector index, then distance metric specified in the vector index is used for both exact and approximate (index-based) searches.

Parameters

  * `expr1` and `expr2` must evaluate to vectors and have the same number of dimensions. This function returns NULL if either `expr1` or `expr2` is NULL or if the dimensions between the two vectors do not match up. 

  * `metric` must be one of the following tokens : 

    * `COSINE` metric is the default metric. It calculates the cosine distane between two vectors. 

    * `DOT` metric, also called the inner product, calculates the negated dot product of two vectors. 

    * `EUCLIDEAN` metric, also called `L2_DISTANCE`, calculates the Euclidean distance between two vectors. 

    * `EUCLIDEAN_SQUARED` metric, also called `L2_SQUARED` is the Euclidean distance without taking the square root. 

    * `HAMMING` metric calculates the hamming distance between two vectors. 

    * `MANHATTAN` metric, also called `L1_DISTANCE` or taxicab distance, calculates the Manhattan distance. 

Shorthand Operators for Distances

Syntax

  * `expr1 <-> expr2`

`<->` is the Euclidian distance operator: `expr1 <-> expr2` is equivalent to
`L2_DISTANCE(expr1, expr2)` or `VECTOR_DISTANCE(expr1, expr2, EUCLIDEAN)`

  * `expr1 <=> expr2`

`<=>` is the cosine distance operator: `expr1 <=> expr2` is equivalent
to`COSINE_DISTANCE(expr1, expr2)` or `VECTOR_DISTANCE(expr1, expr2, COSINE)`

  * `expr1 <#> expr2`

`<#>` is the negative dot product operator: `expr1 <#> expr2` is equivalent to
`-1*INNER_PRODUCT(expr1, expr2)` or `VECTOR_DISTANCE(expr1, expr2, DOT)`

Examples Using Shorthand Operators for Distances

    
    
     '[1, 2]' <-> '[0,1]'
    
    
    v1 <-> '[' || '1,2,3' || ']' is equivalent to v1 <-> '[1, 2, 3]'
    
    
    v1 <-> '[1,2]' is equivalent to L2_DISTANCE(v1, '[1,2]')
    
    
    v1 <=> v2 is equivalent to COSINE_DISTANCE(v1, v2)
    
    
     v1 <#> v2 is equivalent to -1*INNER_PRODUCT(v1, v2)

Examples

`VECTOR_DISTANCE` with metric `EUCLIDEAN` is equivalent to `L2_DISTANCE`:

    
    
    VECTOR_DISTANCE(expr1, expr2, EUCLIDEAN);
    
    
    L2_DISTANCE(expr1, expr2);
    

`VECTOR_DISTANCE` with metric `COSINE` is equivalent to `COSINE_DISTANCE`:

    
    
    VECTOR_DISTANCE(expr1, expr2, COSINE);
    
    
    COSINE_DISTANCE(expr1, expr2);
    

`VECTOR_DISTANCE` with metric `DOT` is equivalent to -1 * `INNER_PRODUCT`:

    
    
    VECTOR_DISTANCE(expr1, expr2, DOT);
    
    
    -1*INNER_PRODUCT(expr1, expr2);

`VECTOR_DISTANCE` with metric `MANHATTAN` is equivalent to `L1_DISTANCE`:

    
    
    VECTOR_DISTANCE(expr1, expr2, MANHATTAN);
    
    
    L1_DISTANCE(expr1, expr2);

See Also:

  * [COSINE_DISTANCE](cosine_distance.md#GUID-2128DC1D-612A-444F-87D8-3D249CD8F12D)

  * [INNER_PRODUCT](inner_product.md#GUID-6AE745CF-93E7-4192-8F80-7B9853DF5B72)

  * [L1_DISTANCE](l1_distance.md#GUID-604A5B68-10AF-48F3-A84F-ED0B90624059)

  * [L2_DISTANCE](l2_distance.md#GUID-2FD8BC27-7614-471F-A4F5-3ED52130A05A)

  * [Vector Functions](Single-Row-Functions.md#GUID-C0C477F1-8210-4CA9-A5FA-0A340C409892)

  * [Vector Distance Metrics of the AI Vector Search User's Guide.](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=VECSE-GUID-DBC136C1-7C63-4B7F-902B-2289FF375560)


[← Previous](vector_chunks.md)

[Next →](vector_dims.md)
