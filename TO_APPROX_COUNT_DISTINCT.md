[Previous](TIMESTAMP_TO_SCN.md) [Next](TO_APPROX_PERCENTILE.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TO_APPROX_COUNT_DISTINCT

## TO_APPROX_COUNT_DISTINCT

Syntax

![Description of to_approx_count_distinct.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_approx_count_distinct.gif)  
[Description of the illustration
to_approx_count_distinct.eps](img_text/to_approx_count_distinct.md)

Purpose

`TO_APPROX_COUNT_DISTINCT` takes as its input a detail containing information
about an approximate distinct value count, and converts it to a `NUMBER`
value.

For `detail`, specify a detail of type `BLOB`, which was created by the
`APPROX_COUNT_DISTINCT_DETAIL` function or the `APPROX_COUNT_DISTINCT_AGG`
function.

See Also:

  * [APPROX_COUNT_DISTINCT_DETAIL](APPROX_COUNT_DISTINCT_DETAIL.md#GUID-8FBD2881-743D-425E-A104-472A720DEF50)

  * [TO_APPROX_COUNT_DISTINCT](TO_APPROX_COUNT_DISTINCT.md#GUID-42A18FFB-C992-44A0-AC3E-F4BBF005846F)

Examples

Refer to [TO_APPROX_COUNT_DISTINCT:
Examples](APPROX_COUNT_DISTINCT_DETAIL.md#GUID-8FBD2881-743D-425E-A104-472A720DEF50__TO_APPROX_COUNT_DISTINCTEXAMPLES-08E8528C)
for examples of using the `TO_APPROX_COUNT_DISTINCT` function in conjunction
with the `APPROX_COUNT_DISTINCT_DETAIL` and `APPROX_COUNT_DISTINCT_AGG`
functions.


[← Previous](TIMESTAMP_TO_SCN.md)

[Next →](TO_APPROX_PERCENTILE.md)
