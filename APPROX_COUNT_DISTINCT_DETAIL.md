[Previous](APPROX_COUNT_DISTINCT_AGG.md) [Next](APPROX_MEDIAN.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. APPROX_COUNT_DISTINCT_DETAIL

## APPROX_COUNT_DISTINCT_DETAIL

Syntax

![Description of approx_count_distinct_detail.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/approx_count_distinct_detail.gif)  
[Description of the illustration
approx_count_distinct_detail.eps](img_text/approx_count_distinct_detail.md)

Purpose

`APPROX_COUNT_DISTINCT_DETAIL` calculates information about the approximate
number of rows that contain a distinct value for expr and returns a BLOB
value, called a detail, which contains that information in a special format.

For `expr`, you can specify a column of any scalar data type other than
`BFILE`, `BLOB`, `CLOB`, `LONG`, `LONG` `RAW`, or `NCLOB`. This function
ignores rows for which the value of `expr` is null.

This function is commonly used with the `GROUP` `BY` clause in a `SELECT`
statement. When used in this way, it calculates approximate distinct value
count information for `expr` within each group of rows and returns a single
detail for each group.

The details returned by `APPROX_COUNT_DISTINCT_DETAIL` can be used as input to
the `APPROX_COUNT_DISTINCT_AGG` function, which enables you to perform
aggregations of the details, or the `TO_APPROX_COUNT_DISTINCT` function, which
converts a detail to a human-readable distinct count value. You can use these
three functions together to perform resource-intensive approximate count
calculations once, store the resulting details, and then perform efficient
aggregations and queries on those details. For example:

  1. Use the `APPROX_COUNT_DISTINCT_DETAIL` function to calculate approximate distinct value count information and store the resulting details in a table or materialized view. These could be highly-granular details, such as city demographic counts or daily sales counts. 

  2. Use the `APPROX_COUNT_DISTINCT_AGG` function to aggregate the details obtained in the previous step and store the resulting details in a table or materialized view. These could be details of lower granularity, such as state demographic counts or monthly sales counts. 

  3. Use the `TO_APPROX_COUNT_DISTINCT` function to convert the stored detail values to human-readable `NUMBER` values. You can use the `TO_APPROX_COUNT_DISTINCT` function to query detail values created by the `APPROX_COUNT_DISTINCT_DETAIL` function or the `APPROX_COUNT_DISTNCT_AGG` function. 

See Also:

  * [APPROX_COUNT_DISTINCT_AGG](APPROX_COUNT_DISTINCT_AGG.md#GUID-EEDA9388-A066-422A-B5C0-639A3076A10B)

  * [TO_APPROX_COUNT_DISTINCT](TO_APPROX_COUNT_DISTINCT.md#GUID-42A18FFB-C992-44A0-AC3E-F4BBF005846F)

Examples

The examples in this section demonstrate how to use the
`APPROX_COUNT_DISTINCT_DETAIL`, `APPROX_COUNT_DISTINCT_AGG`, and
`TO_APPROX_COUNT_DISTINCT` functions together to perform resource-intensive
approximate count calculations once, store the resulting details, and then
perform efficient aggregations and queries on those details.

APPROX_COUNT_DISTINCT_DETAIL: Example

The following statement queries the tables `sh`.`times` and `sh`.`sales` for
the approximate number of distinct products sold each day. The
`APPROX_COUNT_DISTINCT_DETAIL` function returns the information in a detail,
called `daily_detail`, for each day that products were sold. The returned
details are stored in a materialized view called `daily_prod_count_mv`.

    
    
    CREATE MATERIALIZED VIEW daily_prod_count_mv AS
      SELECT t.calendar_year year,
             t.calendar_month_number month,
             t.day_number_in_month day,
             APPROX_COUNT_DISTINCT_DETAIL(s.prod_id) daily_detail
      FROM times t, sales s
      WHERE t.time_id = s.time_id
      GROUP BY t.calendar_year, t.calendar_month_number, t.day_number_in_month;

APPROX_COUNT_DISTINCT_AGG: Examples

The following statement uses the `APPROX_COUNT_DISTINCT_AGG` function to read
the daily details stored in `daily_prod_count_mv` and create aggregated
details that contain the approximate number of distinct products sold each
month. These aggregated details are stored in a materialized view called
`monthly_prod_count_mv`.

    
    
    CREATE MATERIALIZED VIEW monthly_prod_count_mv AS
      SELECT year,
             month,
             APPROX_COUNT_DISTINCT_AGG(daily_detail) monthly_detail
      FROM daily_prod_count_mv
      GROUP BY year, month;

The following statement is similar to the previous statement, except it
creates aggregated details that contain the approximate number of distinct
products sold each year. These aggregated details are stored in a materialized
view called `annual_prod_count_mv`.

    
    
    CREATE MATERIALIZED VIEW annual_prod_count_mv AS
      SELECT year,
             APPROX_COUNT_DISTINCT_AGG(daily_detail) annual_detail
      FROM daily_prod_count_mv
      GROUP BY year;

TO_APPROX_COUNT_DISTINCT: Examples

The following statement uses the `TO_APPROX_COUNT_DISTINCT` function to query
the daily detail information stored in `daily_prod_count_mv` and return the
approximate number of distinct products sold each day:

    
    
    SELECT year,
           month,
           day,
           TO_APPROX_COUNT_DISTINCT(daily_detail) "NUM PRODUCTS"
      FROM daily_prod_count_mv
      ORDER BY year, month, day;
    
          YEAR      MONTH        DAY NUM PRODUCTS
    ---------- ---------- ---------- ------------
          1998          1          1           24
          1998          1          2           25
          1998          1          3           11
          1998          1          4           34
          1998          1          5           10
          1998          1          6            8
          1998          1          7           37
          1998          1          8           26
          1998          1          9           25
          1998          1         10           38
    . . .

The following statement uses the `TO_APPROX_COUNT_DISTINCT` function to query
the monthly detail information stored in `monthly_prod_count_mv` and return
the approximate number of distinct products sold each month:

    
    
    SELECT year,
           month,
           TO_APPROX_COUNT_DISTINCT(monthly_detail) "NUM PRODUCTS"
      FROM monthly_prod_count_mv
      ORDER BY year, month;
    
          YEAR      MONTH NUM PRODUCTS
    ---------- ---------- ------------
          1998          1           57
          1998          2           56
          1998          3           55
          1998          4           49
          1998          5           49
          1998          6           48
          1998          7           54
          1998          8           56
          1998          9           55
          1998         10           57
    . . .

The following statement uses the `TO_APPROX_COUNT_DISTINCT` function to query
the annual detail information stored in `annual_prod_count_mv` and return the
approximate number of distinct products sold each year:

    
    
    SELECT year,
           TO_APPROX_COUNT_DISTINCT(annual_detail) "NUM PRODUCTS"
      FROM annual_prod_count_mv
      ORDER BY year;
    
          YEAR NUM PRODUCTS
    ---------- ------------
          1998           60
          1999           72
          2000           72
          2001           71


[← Previous](APPROX_COUNT_DISTINCT_AGG.md)

[Next →](APPROX_MEDIAN.md)
