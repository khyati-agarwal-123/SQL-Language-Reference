[Previous](Aggregate-Functions.md) [Next](Data-Cartridge-Functions.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. Analytic Functions 

## Analytic Functions

Analytic functions compute an aggregate value based on a group of rows. They
differ from aggregate functions in that they return multiple rows for each
group. The group of rows is called a window and is defined by the
`analytic_clause`. For each row, a sliding window of rows is defined. The
window determines the range of rows used to perform the calculations for the
current row. Window sizes can be based on either a physical number of rows or
a logical interval such as time.

Analytic functions are the last set of operations performed in a query except
for the final `ORDER` `BY` clause. All joins and all `WHERE`, `GROUP` `BY`,
and `HAVING` clauses are completed before the analytic functions are
processed. Therefore, analytic functions can appear only in the select list or
`ORDER` `BY` clause.

Analytic functions are commonly used to compute cumulative, moving, centered,
and reporting aggregates.

analytic_function::=

![Description of analytic_function.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/analytic_function.gif)  
[Description of the illustration
analytic_function.eps](img_text/analytic_function.md)

analytic_clause::=

![Description of analytic_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/analytic_clause.gif)  
[Description of the illustration
analytic_clause.eps](img_text/analytic_clause.md)

query_partition_clause::=

![Description of query_partition_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/query_partition_clause.gif)  
[Description of the illustration
query_partition_clause.eps](img_text/query_partition_clause.md)

order_by_clause::=

![Description of order_by_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/order_by_clause.gif)  
[Description of the illustration
order_by_clause.eps](img_text/order_by_clause.md)

windowing_clause::=

![Description of windowing_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/windowing_clause.gif)  
[Description of the illustration
windowing_clause.eps](img_text/windowing_clause.md)

The semantics of this syntax are discussed in the sections that follow.

analytic_function

Specify the name of an analytic function (see the listing of analytic
functions following this discussion of semantics).

arguments

Analytic functions take 0 to 3 arguments. The arguments can be any numeric
data type or any nonnumeric data type that can be implicitly converted to a
numeric data type. Oracle determines the argument with the highest numeric
precedence and implicitly converts the remaining arguments to that data type.
The return type is also that data type, unless otherwise noted for an
individual function.

See Also:

[Numeric Precedence](Data-
Types.md#GUID-4C0B65DB-E751-4957-A1ED-5044BAFA7812) for information on
numeric precedence and [Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion

analytic_clause

Use `OVER` `analytic_clause` to indicate that the function operates on a query
result set. This clause is computed after the `FROM`, `WHERE`, `GROUP` `BY`,
and `HAVING` clauses. You can specify analytic functions with this clause in
the select list or `ORDER` `BY` clause. To filter the results of a query based
on an analytic function, nest these functions within the parent query, and
then filter the results of the nested subquery.

Notes on the analytic_clause:

The following notes apply to the `analytic_clause`:

  * You cannot nest analytic functions by specifying any analytic function in any part of the `analytic_clause`. However, you can specify an analytic function in a subquery and compute another analytic function over it. 

  * You can specify `OVER` `analytic_clause` with user-defined analytic functions as well as built-in analytic functions. See [CREATE FUNCTION](CREATE-FUNCTION.md#GUID-156AEDAC-ADD0-4E46-AA56-6D1F7CA63306). 

  * The `PARTITION` `BY` and `ORDER` `BY` clauses in the `analytic_clause` are collation-sensitive. 

See Also:

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation determination rules for the `OVER` `(PARTITION` `BY` ... `ORDER` `BY` ... `)` clause of an analytic function 

  * [`window_clause`](SELECT.md#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6__GUID-911420AB-72C0-42DC-8D84-8C87171996ED) in the `SELECT` statement 

query_partition_clause

Use the `PARTITION` `BY` clause to partition the query result set into groups
based on one or more `value_expr`. If you omit this clause, then the function
treats all rows of the query result set as a single group.

To use the `query_partition_clause` in an analytic function, use the upper
branch of the syntax (without parentheses). To use this clause in a model
query (in the `model_column_clauses`) or a partitioned outer join (in the
`outer_join_clause`), use the lower branch of the syntax (with parentheses).

You can specify multiple analytic functions in the same query, each with the
same or different `PARTITION` `BY` keys.

If the objects being queried have the parallel attribute, and if you specify
an analytic function with the `query_partition_clause`, then the function
computations are parallelized as well.

Valid values of `value_expr` are constants, columns, nonanalytic functions,
function expressions, or expressions involving any of these.

order_by_clause

Use the `order_by_clause` to specify how data is ordered within a partition.
For all analytic functions you can order the values in a partition on multiple
keys, each defined by a `value_expr` and each qualified by an ordering
sequence.

Within each function, you can specify multiple ordering expressions. Doing so
is especially useful when using functions that rank values, because the second
expression can resolve ties between identical values for the first expression.

Whenever the `order_by_clause` results in identical values for multiple rows,
the function behaves as follows:

  * `CUME_DIST`, `DENSE_RANK`, `NTILE`, `PERCENT_RANK`, and `RANK` return the same result for each of the rows. 

  * `ROW_NUMBER` assigns each row a distinct value even if there is a tie based on the `order_by_clause`. The value is based on the order in which the row is processed, which may be nondeterministic if the `ORDER` `BY` does not guarantee a total ordering. 

  * For all other analytic functions, the result depends on the window specification. If you specify a logical window with the `RANGE` keyword, then the function returns the same result for each of the rows. If you specify a physical window with the `ROWS` keyword, then the result is nondeterministic. 

Restrictions on the ORDER BY Clause

The following restrictions apply to the `ORDER` `BY` clause:

  * When used in an analytic function, the `order_by_clause` must take an expression (`expr`). The `SIBLINGS` keyword is not valid (it is relevant only in hierarchical queries). Position (`position`) and column aliases (`c_alias`) are also invalid. Otherwise this `order_by_clause` is the same as that used to order the overall query or subquery. 

  * An analytic function that uses the `RANGE` keyword can use multiple sort keys in its `ORDER` `BY` clause if it specifies any of the following windows: 

    * `RANGE` `BETWEEN` `UNBOUNDED` `PRECEDING` `AND` `CURRENT` `ROW`. The short form of this is `RANGE` `UNBOUNDED` `PRECEDING`. 

    * `RANGE` `BETWEEN` `CURRENT` `ROW` `AND` `UNBOUNDED` `FOLLOWING`

    * `RANGE` `BETWEEN` `CURRENT` `ROW` `AND` `CURRENT` `ROW`

    * `RANGE` `BETWEEN` `UNBOUNDED` `PRECEDING` `AND` `UNBOUNDED` `FOLLOWING`

Window boundaries other than these four can have only one sort key in the
`ORDER` `BY` clause of the analytic function. This restriction does not apply
to window boundaries specified by the `ROW` keyword.

ASC | DESC

Specify the ordering sequence (ascending or descending). `ASC` is the default.

NULLS FIRST | NULLS LAST

Specify whether returned rows containing nulls should appear first or last in
the ordering sequence.

`NULLS` `LAST` is the default for ascending order, and `NULLS` `FIRST` is the
default for descending order.

Analytic functions always operate on rows in the order specified in the
`order_by_clause` of the function. However, the `order_by_clause` of the
function does not guarantee the order of the result. Use the `order_by_clause`
of the query to guarantee the final result ordering.

See Also:

[order_by_clause](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2171079) of [SELECT](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6) for more information on this clause

windowing_clause

Some analytic functions allow the `windowing_clause`. In the listing of
analytic functions at the end of this section, the functions that allow the
`windowing_clause` are followed by an asterisk (*).

ROWS | RANGE | GROUPS

The keywords `ROWS`, `RANGE`, and `GROUPS` are options to define a window
frame unit used for calculating the function result. The function is then
applied to all the rows in the window. The window moves through the query
result set or partition from top to bottom.

  * Use `ROWS` to specify the window frame extent by counting rows forward or backward from the current row. `ROWS` allows any number of sort keys, of any ordered data types. 

  * Use `RANGE` to specify the window frame extent as a logical offset. `RANGE` allows only one sort key, and its declared data type must allow addition and subtraction operations, for example they must be numeric, datetime, or interval data types. 

  * Use `GROUPS` to specifiy the window frame extent with both `ROWS` and `RANGE` characteristics. Like `ROWS` a `GROUPS` window can have any number of sort keys, or any ordered types. Like `RANGE`, a `GROUPS` window does not make cutoffs between adjacent rows with the same values in the sort keys. 

You cannot specify this clause unless you have specified the
`order_by_clause`. Some window boundaries defined by the `RANGE` clause let
you specify only one expression in the `order_by_clause`. Refer to
[Restrictions on the ORDER BY Clause](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056__CIHCEIGA).

The value returned by an analytic function with a logical offset is always
deterministic. However, the value returned by an analytic function with a
physical offset may produce nondeterministic results unless the ordering
expression results in a unique ordering. You may have to specify multiple
columns in the `order_by_clause` to achieve this unique ordering.

BETWEEN ... AND

Use the `BETWEEN` ... `AND` clause to specify a start point and end point for
the window. The first expression (before `AND`) defines the start point and
the second expression (after `AND`) defines the end point.

If you omit `BETWEEN` and specify only one end point, then Oracle considers it
the start point, and the end point defaults to the current row.

UNBOUNDED PRECEDING

Specify `UNBOUNDED` `PRECEDING` to indicate that the window starts at the
first row of the partition. This is the start point specification and cannot
be used as an end point specification.

UNBOUNDED FOLLOWING

Specify `UNBOUNDED` `FOLLOWING` to indicate that the window ends at the last
row of the partition. This is the end point specification and cannot be used
as a start point specification.

CURRENT ROW

As a start point, `CURRENT` `ROW` specifies that the window begins at the
current row or value (depending on whether you have specified `ROW` or
`RANGE`, respectively). In this case the end point cannot be `value_expr`
`PRECEDING`.

As an end point, `CURRENT` `ROW` specifies that the window ends at the current
row or value (depending on whether you have specified `ROW` or `RANGE`,
respectively). In this case the start point cannot be `value_expr`
`FOLLOWING`.

value_expr PRECEDING or value_expr FOLLOWING

For `RANGE` or `ROW`:

  * If `value_expr` `FOLLOWING` is the start point, then the end point must be `value_expr` `FOLLOWING`. 

  * If `value_expr` `PRECEDING` is the end point, then the start point must be `value_expr` `PRECEDING`. 

If you are defining a logical window defined by an interval of time in numeric
format, then you may need to use conversion functions.

See Also:

[NUMTOYMINTERVAL](NUMTOYMINTERVAL.md#GUID-B98B21AA-44F7-4A9D-A646-6775A1D5F46D)
and
[NUMTODSINTERVAL](NUMTODSINTERVAL.md#GUID-5A7392A8-7976-4465-8839-A65EFF1A80B6)
for information on converting numeric times into intervals

If you specified `ROWS`:

  * `value_expr` is a physical offset. It must be a constant or expression and must evaluate to a positive numeric value. 

  * If `value_expr` is part of the start point, then it must evaluate to a row before the end point. 

If you specified `RANGE`:

  * `value_expr` is a logical offset. It must be a constant or expression that evaluates to a positive numeric value or an interval literal. Refer to [Literals](Literals.md#GUID-192417E8-A79D-4A1D-9879-68272D925707) for information on interval literals. 

  * You can specify only one expression in the `order_by_clause`. 

  * If `value_expr` evaluates to a numeric value, then the `ORDER` `BY` `expr` must be a numeric or `DATE` data type. 

  * If `value_expr` evaluates to an interval value, then the `ORDER` `BY` `expr` must be a `DATE` data type. 

If you omit the `windowing_clause` entirely, then the default is `RANGE`
`BETWEEN` `UNBOUNDED` `PRECEDING` `AND` `CURRENT` `ROW`.

EXCLUDE

You can remove rows, groups, and ties from the window frame with the `EXCLUDE`
options:

  * If you specify `EXCLUDE CURRENT ROW`, and the current row in in the window frame, then the current row is removed from the window frame. 

  * If you specify `EXCLUDE GROUP`, then the current row and any peers of the current row are removed from the window frame. 

  * If you specify `EXCLUDE TIES`, then the peers of the current row are removed from the window frame. The current row is retained. Note, that if the current row is previously removed from the window frame, it remains removed. 

  * If you specify `EXCLUDE NO OTHERS`, then no additional rows are removed from the window frame. This is the default option. 

Analytic functions are commonly used in data warehousing environments. In the
list of analytic functions that follows, functions followed by an asterisk (*)
allow the full syntax, including the `windowing_clause`.

  * [AVG](AVG.md#GUID-B64BCBF1-DAA0-4D88-9821-2C4D3FDE5E4A) * 
  * [BIT_AND_AGG](BIT_AND_AGG.md#GUID-82497098-6D77-48D3-89EF-C1041BF8A258)* 
  * [BIT_OR_AGG](BIT_OR_AGG.md#GUID-18B0E3CB-1C90-4625-8E36-B422FA4E04A8)* 
  * [BIT_XOR_AGG](BIT_XOR_AGG.md#GUID-1563FB7E-9CC9-4D03-859E-BE336AF01F1D)* 
  * [BOOLEAN_AND_AGG](boolean_and_agg.md#GUID-AF3C1A26-C7A1-4BD2-B15C-86B761D4D8D9)* 
  * [BOOLEAN_OR_AGG](boolean_or_agg.md#GUID-C3E187DE-BD26-4440-B0AD-51342FFA4775)* 
  * [CHECKSUM](checksum.md#GUID-3F55C5DF-F23A-4B2F-BC6F-E03B34B78BA8)* 
  * [CLUSTER_DETAILS](CLUSTER_DETAILS.md#GUID-6E47A5A7-B73A-4D79-BAA5-BB7E3C173D0F)
  * [CLUSTER_DISTANCE](CLUSTER_DISTANCE.md#GUID-21E611E3-2F15-4DF1-B648-9A36E8D5CE4D)
  * [CLUSTER_ID](CLUSTER_ID.md#GUID-1B0D0954-5A57-409C-9E84-F3EE12712040)
  * [CLUSTER_PROBABILITY](CLUSTER_PROBABILITY.md#GUID-999A15BA-FEDD-4FA6-8F1B-C847C2FE51CD)
  * [CLUSTER_SET](CLUSTER_SET.md#GUID-7B44CB7A-4783-4FE0-80D8-26AE88D6B060)
  * [CORR](CORR.md#GUID-E73AF5E2-38A4-436A-955C-5122C079F49C) * 
  * [COUNT](COUNT.md#GUID-AEF08B79-024D-4E3A-B362-9715FB011776) * 
  * [COVAR_POP](COVAR_POP.md#GUID-D728D05F-D2E3-405C-986F-088B8353553A) * 
  * [COVAR_SAMP](COVAR_SAMP.md#GUID-7850B9E1-83A4-41CB-8F17-DCD2E2A70C95) * 
  * [CUME_DIST](CUME_DIST.md#GUID-B12C577C-A63C-4D19-8E18-FCCBBFBF8278)
  * [DENSE_RANK](DENSE_RANK.md#GUID-BB66F574-09DF-4594-87A4-ABD83E8DC3FE)
  * [EVERY](every.md#GUID-C34D8A50-3050-4F32-941A-8C2512DEC62D)* 
  * [FEATURE_DETAILS](FEATURE_DETAILS.md#GUID-A42F313B-22C1-4CAC-BA3F-C418178D743F)
  * [FEATURE_ID](FEATURE_ID.md#GUID-BA187F80-5F51-49F6-BB69-64422FB9FD90)
  * [FEATURE_SET](FEATURE_SET.md#GUID-55582346-F1D6-447E-851A-D4912982EB28)
  * [FEATURE_VALUE](FEATURE_VALUE.md#GUID-EC0E44D0-BE01-49F8-9E5A-72B500119877)
  * [FIRST](FIRST.md#GUID-85AB9246-0E0A-44A1-A7E6-4E57502E9238)
  * [FIRST_VALUE](FIRST_VALUE.md#GUID-D454EC3F-370C-4C64-9B11-33FCB10D95EC) * 
  * [KURTOSIS_POP](KURTOSIS_POP.md#GUID-F820DFF7-B758-460E-AECC-053915069B9F)* 
  * [KURTOSIS_SAMP](KURTOSIS_SAMP.md#GUID-487DE503-A015-415F-B6CD-F9D095B91178)* 
  * [LAG](LAG.md#GUID-68081CD0-72BE-4C0A-AA6B-AD39FFA7BCF2)
  * [LAST](LAST.md#GUID-4E16BC0E-D3B8-4BA4-8F97-3A08891A85CC)
  * [LAST_VALUE](LAST_VALUE.md#GUID-A646AF95-C8E9-4A67-87BA-87B11AEE7B79) * 
  * [LEAD](LEAD.md#GUID-0A0481F1-E98F-4535-A739-FCCA8D1B5B77)
  * [LISTAGG](LISTAGG.md#GUID-B6E50D8E-F467-425B-9436-F7F8BF38D466)
  * [MAX](MAX.md#GUID-E5372020-A6DA-44BF-93BE-DA8C3F74CD01) * 
  * [MEDIAN](MEDIAN.md#GUID-DE15705A-AC18-4416-8487-B9E1D70CE01A)
  * [MIN](MIN.md#GUID-F7F04E18-1AD8-4D15-9491-4622AD847A74) * 
  * [NTH_VALUE](NTH_VALUE.md#GUID-F8A0E88C-67E5-4AA6-9515-95D03A7F9EA0) * 
  * [NTILE](NTILE.md#GUID-FAD7A986-AEBD-4A03-B0D2-F7F2148BA5E9)
  * [PERCENT_RANK](PERCENT_RANK.md#GUID-66A868F5-9EBA-482A-BF8C-09300B9EE165)
  * [PERCENTILE_CONT](PERCENTILE_CONT.md#GUID-CA259452-A565-41B3-A4F4-DD74B66CEDE0)
  * [PERCENTILE_DISC](PERCENTILE_DISC.md#GUID-7C34FDDA-C241-474F-8C5C-50CC0182E005)
  * [PREDICTION](PREDICTION.md#GUID-DA66A1C3-BFB2-43A1-A3FF-93D4A3DAB9C6)
  * [PREDICTION_COST](PREDICTION_COST.md#GUID-2E58222D-FB7E-4CA2-BCAA-C932FCDEE890)
  * [PREDICTION_DETAILS](PREDICTION_DETAILS.md#GUID-D7261A56-E729-4882-B48D-CDD343C53810)
  * [PREDICTION_PROBABILITY](PREDICTION_PROBABILITY.md#GUID-0F309771-40A3-4E23-9A96-CD134C80F584)
  * [PREDICTION_SET](PREDICTION_SET.md#GUID-25AE84A7-C733-4BC5-8C57-2E5574C49AFC)
  * [RANK](RANK.md#GUID-0950BD34-C994-41DA-A8F9-34B3FE53BBBA)
  * [RATIO_TO_REPORT](RATIO_TO_REPORT.md#GUID-9D10C275-4341-435F-ACF4-767B9CCB7390)
  * [REGR_ (Linear Regression) Functions](REGR_-Linear-Regression-Functions.md#GUID-A675B68F-2A88-4843-BE2C-FCDE9C65F9A9) * 
  * [ROW_NUMBER](ROW_NUMBER.md#GUID-D5A157F8-0F53-45BD-BF8C-AE79B1DB8C41)
  * [STDDEV](STDDEV.md#GUID-CA0C3B1F-1A4C-4CFB-ADAB-D90216C4E099) * 
  * [SKEWNESS_POP](SKEWNESS_POP.md#GUID-DF34158F-B681-4933-BA27-0A3885A9F43C)* 
  * [SKEWNESS_SAMP](SKEWNESS_SAMP.md#GUID-E71D9AEC-0AAA-4A6C-BF70-29EE9AD8F7EC)* 
  * [STDDEV_POP](STDDEV_POP.md#GUID-4F804DE5-7E20-4E08-A1BA-32DBB167B34B) * 
  * [STDDEV_SAMP](STDDEV_SAMP.md#GUID-7B2A708E-E73A-4CFE-978E-3F9C4BD37467) * 
  * [SUM](SUM.md#GUID-5610BE2C-CFE5-446F-A1F7-B924B5663220) * 
  * [VAR_POP](VAR_POP.md#GUID-B62FB4A4-BD1F-47B0-B412-31A98B70C2E4) * 
  * [VAR_SAMP](VAR_SAMP.md#GUID-314D5831-0E26-4ABF-9F46-35F78F97DA52) * 
  * [VARIANCE](VARIANCE.md#GUID-EC33717A-2509-402D-B3BB-7EECB2E4ED8B) * 

See Also:

[Oracle Database Data Warehousing
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DWHSG021) for more information on these functions and for
scenarios illustrating their use


[← Previous](Aggregate-Functions.md)

[Next →](Data-Cartridge-Functions.md)
