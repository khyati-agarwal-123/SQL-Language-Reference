[Previous](APPROX_COUNT_DISTINCT.md)
[Next](APPROX_COUNT_DISTINCT_DETAIL.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. APPROX_COUNT_DISTINCT_AGG

## APPROX_COUNT_DISTINCT_AGG

Syntax

![Description of approx_count_distinct_agg.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/approx_count_distinct_agg.gif)  
[Description of the illustration
approx_count_distinct_agg.eps](img_text/approx_count_distinct_agg.md)

Purpose

`APPROX_COUNT_DISTINCT_AGG` takes as its input a column of details containing
information about approximate distinct value counts, and enables you to
perform aggregations of those counts.

For `detail`, specify a column of details created by the
`APPROX_COUNT_DISTINCT_DETAIL` function or the `APPROX_COUNT_DISTINCT_AGG`
function. This column is of data type `BLOB`.

You can specify this function in a `SELECT` statement with a `GROUP` `BY`
clause to aggregate the information contained in the details within each group
of rows and return a single detail for each group.

This function returns a `BLOB` value, called a detail, which contains
information about the count aggregations in a special format. You can store
details returned by this function in a table or materialized view, and then
again use the `APPROX_COUNT_DISTINCT_AGG` function to further aggregate those
details, or use the `TO_APPROX_COUNT_DISTINCT` function to convert the detail
values to human-readable `NUMBER` values.

See Also:

  * [APPROX_COUNT_DISTINCT_DETAIL](APPROX_COUNT_DISTINCT_DETAIL.md#GUID-8FBD2881-743D-425E-A104-472A720DEF50)

  * [TO_APPROX_COUNT_DISTINCT](TO_APPROX_COUNT_DISTINCT.md#GUID-42A18FFB-C992-44A0-AC3E-F4BBF005846F)

Examples

Refer to [APPROX_COUNT_DISTINCT_AGG:
Examples](APPROX_COUNT_DISTINCT_DETAIL.md#GUID-8FBD2881-743D-425E-A104-472A720DEF50__APPROX_COUNT_DISTINCT_AGGEXAMPLES-08E84F63)
for examples of using the `APPROX_COUNT_DISTINCT_AGG` function in conjunction
with the `APPROX_COUNT_DISTINCT_DETAIL` and `TO_APPROX_COUNT_DISTINCT`
functions.


[← Previous](APPROX_COUNT_DISTINCT.md)

[Next →](APPROX_COUNT_DISTINCT_DETAIL.md)
