[Previous](APPROX_PERCENTILE.md) [Next](APPROX_PERCENTILE_DETAIL.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. APPROX_PERCENTILE_AGG

## APPROX_PERCENTILE_AGG

Syntax

![Description of approx_percentile_agg.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/approx_percentile_agg.gif)  
[Description of the illustration
approx_percentile_agg.eps](img_text/approx_percentile_agg.md)

Purpose

`APPROX_PERCENTILE_AGG` takes as its input a column of details containing
approximate percentile information, and enables you to perform aggregations of
that information.

For `detail`, specify a column of details created by the
`APPROX_PERCENT_DETAIL` function or the `APPROX_PERCENTILE_AGG` function. This
column is of data type `BLOB`.

You can specify this function in a `SELECT` statement with a `GROUP` `BY`
clause to aggregate the information contained in the details within each group
of rows and return a single detail for each group.

This function returns a `BLOB` value, called a detail, which contains
approximate percentile information in a special format. You can store details
returned by this function in a table or materialized view, and then again use
the `APPROX_PERCENTILE_AGG` function to further aggregate those details, or
use the `TO_APPROX_PERCENTILE` function to convert the details to specified
percentile values.

See Also:

  * [APPROX_PERCENTILE_DETAIL](APPROX_PERCENTILE_DETAIL.md#GUID-F9A0B9B5-671F-43CA-9FA7-69A2DD174F54)

  * [TO_APPROX_PERCENTILE](TO_APPROX_PERCENTILE.md#GUID-463702B2-9199-41ED-AE03-865CABAD3E23)

Examples

Refer to [APPROX_PERCENTILE_AGG:
Examples](APPROX_PERCENTILE_DETAIL.md#GUID-F9A0B9B5-671F-43CA-9FA7-69A2DD174F54__APPROX_PERCENTILE_AGGEXAMPLES-088B7917)
for examples of using the `APPROX_PERCENTILE_AGG` function in conjunction with
the `APPROX_PERCENTILE_DETAIL` and `TO_APPROX_PERCENTILE` functions.


[← Previous](APPROX_PERCENTILE.md)

[Next →](APPROX_PERCENTILE_DETAIL.md)
