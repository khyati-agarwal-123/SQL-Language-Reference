[Previous](PREDICTION_BOUNDS.md) [Next](PREDICTION_DETAILS.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. PREDICTION_COST 

## PREDICTION_COST

Syntax

prediction_cost::=

![Description of prediction_cost.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/prediction_cost.gif)  
[Description of the illustration
prediction_cost.eps](img_text/prediction_cost.md)

prediction_cost_ordered::=

![Description of prediction_cost_ordered.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/prediction_cost_ordered.gif)  
[Description of the illustration
prediction_cost_ordered.eps](img_text/prediction_cost_ordered.md)

Analytic Syntax

prediction_cost_analytic::=

![Description of prediction_cost_analytic.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/prediction_cost_analytic.gif)  
[Description of the illustration
prediction_cost_analytic.eps](img_text/prediction_cost_analytic.md)

cost_matrix_clause::=

![Description of cost_matrix_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cost_matrix_clause.gif)  
[Description of the illustration
cost_matrix_clause.eps](img_text/cost_matrix_clause.md)

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

"[Analytic Functions](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056)" for information on
the syntax, semantics, and restrictions of `mining_analytic_clause`

Purpose

`PREDICTION_COST` returns a cost for each row in the selection. The cost
refers to the lowest cost class or to the specified `class`. The cost is
returned as `BINARY_DOUBLE`.

`PREDICTION_COST` can perform classification or anomaly detection. For
classification, the returned cost refers to a predicted target class. For
anomaly detection, the returned cost refers to a classification of `1` (for
typical rows) or `0` (for anomalous rows).

You can use `PREDICTION_COST` in conjunction with the `PREDICTION` function to
obtain the prediction and the cost of the prediction.

cost_matrix_clause

Costs are a biasing factor for minimizing the most harmful kinds of
misclassifications. For example, false positives might be considered more
costly than false negatives. Costs are specified in a cost matrix that can be
associated with the model or defined inline in a `VALUES` clause. All
classification algorithms can use costs to influence scoring.

Decision Tree is the only algorithm that can use costs to influence the model
build. The cost matrix used to build a Decision Tree model is also the default
scoring cost matrix for the model.

The following cost matrix table specifies that the misclassification of `1` is
five times more costly than the misclassification of `0`.

    
    
    ACTUAL_TARGET_VALUE PREDICTED_TARGET_VALUE       COST
    ------------------- ---------------------- ----------
                      0                      0          0
                      0                      1          1
                      1                      0          5
                      1                      1          0
    

In `cost_matrix_clause`:

  * `COST` `MODEL` indicates that scoring should be performed by taking into account the scoring cost matrix associated with the model. If the cost matrix does not exist, then the function returns an error. 

  * `COST` `MODEL` `AUTO` indicates that the existence of a cost matrix is unknown. If a cost matrix exists, then the function uses it to return the lowest cost prediction. Otherwise the function returns the highest probability prediction. 

  * The `VALUES` clause specifies an inline cost matrix for `class_value`. For example, you could specify that the misclassification of `1` is five times more costly than the misclassification of `0` as follows: 
    
           PREDICTION (nb_model COST (0,1) VALUES ((0, 1),(1, 5)) USING *)
    

If a model that has a scoring cost matrix is invoked with an inline cost
matrix, then the inline costs are used.

See Also:

[Oracle Machine Learning for SQL Userâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DMPRG243) for more information about cost-sensitive
prediction.

Syntax Choice

`PREDICTION_COST` can score the data by applying a mining model object to the
data, or it can dynamically mine the data by executing an analytic clause that
builds and applies one or more transient mining models. Choose Syntax or
Analytic Syntax:

  * Syntax: Use the `prediction_cost` syntax to score the data with a pre-defined model. Supply the name of a model that performs classification or anomaly detection. 

Use the `prediction_cost_ordered` syntax for a model that requires ordered
data, such as an MSET-SPRT model. The `prediction_cost_ordered` syntax
requires an `order_by_clause` clause.

Restrictions on the `prediction_cost_ordered` syntax are that you cannot use
it in the `WHERE` clause of a query. Also, you cannot use a
`query_partition_clause` or a `windowing_clause` with the `prediction_ordered`
syntax.

  * Analytic Syntax: Use the analytic syntax to score the data without a pre-defined model. The analytic syntax uses `mining_analytic_clause` , which specifies if the data should be partitioned for multiple model builds. The `mining_analytic_clause` supports a `query_partition_clause` and an `order_by_clause`. (See "[analytic_clause::=](Analytic-Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056__CJAFAAIA)".) 

    * For classification, specify `FOR` `expr`, where `expr` is an expression that identifies a target column that has a character data type. 

    * For anomaly detection, specify the keywords `OF ANOMALY`. 

The syntax of the `PREDICTION_COST` function can use an optional `GROUPING`
hint when scoring a partitioned model. See [GROUPING
Hint](Comments.md#GUID-9693C230-2616-4123-A1ED-3C41E9566F7A).

mining_attribute_clause

`mining_attribute_clause` identifies the column attributes to use as
predictors for scoring. When the function is invoked with the analytic syntax,
these predictors are also used for building the transient models. The
`mining_attribute_clause` behaves as described for the `PREDICTION` function.
(See "[mining_attribute_clause::=](PREDICTION.md#GUID-
DA66A1C3-BFB2-43A1-A3FF-93D4A3DAB9C6__CJAIGCFC)".)

See Also:

  * [Oracle Machine Learning for SQL Userâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DMPRG004) for information about scoring. 

  * [Oracle Machine Learning for SQL Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DMCON050) for information about classification with costs 

Note:

The following example is excerpted from the Oracle Machine Learning for SQL
sample programs. For more information about the sample programs, see Appendix
A in [Oracle Machine Learning for SQL Userâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DMPRG714).

Example

This example predicts the ten customers in Italy who would respond to the
least expensive sales campaign (offering an affinity card).

    
    
    SELECT cust_id 
    FROM (SELECT cust_id,rank()
           OVER (ORDER BY PREDICTION_COST(DT_SH_Clas_sample, 1 COST MODEL USING *)
                ASC, cust_id) rnk
            FROM mining_data_apply_v
            WHERE country_name = 'Italy')
      WHERE rnk <= 10
      ORDER BY rnk;
     
       CUST_ID
    ----------
        100081
        100179
        100185
        100324
        100344
        100554
        100662
        100733
        101250
        101306


[← Previous](PREDICTION_BOUNDS.md)

[Next →](PREDICTION_DETAILS.md)
