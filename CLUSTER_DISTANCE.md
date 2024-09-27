[Previous](CLUSTER_DETAILS.md) [Next](CLUSTER_ID.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. CLUSTER_DISTANCE 

## CLUSTER_DISTANCE

Syntax

cluster_distance::=

![Description of cluster_distance.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cluster_distance.gif)  
[Description of the illustration
cluster_distance.eps](img_text/cluster_distance.md)

Analytic Syntax

cluster_distance_analytic::=

![Description of cluster_distance_analytic.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cluster_distance_analytic.gif)  
[Description of the illustration
cluster_distance_analytic.eps](img_text/cluster_distance_analytic.md)

mining_attribute_clause::=

![Description of mining_attribute_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/mining_attribute_clause.gif)  
[Description of the illustration
mining_attribute_clause.eps](img_text/mining_attribute_clause.md)

mining_analytic_clause::=

![Description of mining_analytic_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/mining_analytic_clause.gif)  
[Description of the illustration
mining_analytic_clause.eps](img_text/mining_analytic_clause.md)

See Also:

[Analytic Functions](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056) for information on
the syntax, semantics, and restrictions of `mining_analytic_clause`

Purpose

`CLUSTER_DISTANCE` returns a cluster distance for each row in the selection.
The cluster distance is the distance between the row and the centroid of the
highest probability cluster or the specified `cluster_id`. The distance is
returned as `BINARY_DOUBLE`.

Syntax Choice

`CLUSTER_DISTANCE` can score the data in one of two ways: It can apply a
mining model object to the data, or it can dynamically mine the data by
executing an analytic clause that builds and applies one or more transient
mining models. Choose Syntax or Analytic Syntax:

  * Syntax â Use the first syntax to score the data with a pre-defined model. Supply the name of a clustering model. 

  * Analytic Syntax â Use the analytic syntax to score the data without a pre-defined model. Include `INTO` `n`, where `n` is the number of clusters to compute, and `mining_analytic_clause`, which specifies if the data should be partitioned for multiple model builds. The `mining_analytic_clause` supports a `query_partition_clause` and an `order_by_clause`. (See [analytic_clause::=](Analytic-Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056__CJAFAAIA).) 

The syntax of the `CLUSTER_DISTANCE` function can use an optional `GROUPING`
hint when scoring a partitioned model. See [GROUPING
Hint](Comments.md#GUID-9693C230-2616-4123-A1ED-3C41E9566F7A).

mining_attribute_clause

`mining_attribute_clause` identifies the column attributes to use as
predictors for scoring. When the function is invoked with the analytic syntax,
this data is also used for building the transient models. The
`mining_attribute_clause` behaves as described for the `PREDICTION` function.
(See [mining_attribute_clause::=](PREDICTION.md#GUID-
DA66A1C3-BFB2-43A1-A3FF-93D4A3DAB9C6__CJAIGCFC).)

See Also:

  * [Oracle Machine Learning for SQL Userâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DMPRG004) for information about scoring. 

  * [Oracle Machine Learning for SQL Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DMCON008) for information about clustering. 

Note:

The following example is excerpted from the Oracle Machine Learning for SQL
sample programs. For more information about the sample programs, see Appendix
A in [Oracle Machine Learning for SQL Userâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DMPRG714).

Example

This example finds the 10 rows that are most anomalous as measured by their
distance from their nearest cluster centroid.

    
    
    SELECT cust_id
      FROM (
        SELECT cust_id,
               rank() over
                 (order by CLUSTER_DISTANCE(km_sh_clus_sample USING *) desc) rnk
          FROM mining_data_apply_v)
      WHERE rnk <= 11
      ORDER BY rnk;
     
       CUST_ID
    ----------
        100579
        100050
        100329
        100962
        101251
        100179
        100382
        100713
        100629
        100787
        101478


[← Previous](CLUSTER_DETAILS.md)

[Next →](CLUSTER_ID.md)
