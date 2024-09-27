[Previous](INITCAP.md) [Next](INSTR.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. INNER_PRODUCT

## INNER_PRODUCT

Syntax

  

![Description of inner_product.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/inner_product.gif)  
[Description of the illustration
inner_product.eps](img_text/inner_product.md)

  

Purpose

`INNER_PRODUCT` is a shorthand version of the `VECTOR_DISTANCE` function that
calculates the distance between two vectors. It takes two vectors as input and
returns the distance between them as a `BINARY_DOUBLE`.

Parameters

  * `expr1` and `expr2` must evaluate to vectors and have the same number of dimensions. 

  * `INNER_PRODUCT` returns NULL, if either `expr1` or `expr2` is NULL, or if the dimensions between the two vectors do not match up. 

See Also:

  * [VECTOR_DISTANCE](vector_distance.md#GUID-BA4BCFB2-D905-43DC-87B0-E53522CF07B7)

  * [COSINE_DISTANCE](cosine_distance.md#GUID-2128DC1D-612A-444F-87D8-3D249CD8F12D)

  * [L1_DISTANCE](l1_distance.md#GUID-604A5B68-10AF-48F3-A84F-ED0B90624059)

  * [L2_DISTANCE](l2_distance.md#GUID-2FD8BC27-7614-471F-A4F5-3ED52130A05A)

  * [Vector Functions](Single-Row-Functions.md#GUID-C0C477F1-8210-4CA9-A5FA-0A340C409892)


[← Previous](INITCAP.md)

[Next →](INSTR.md)
