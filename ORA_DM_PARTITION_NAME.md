[Previous](NVL2.md) [Next](ORA_DST_AFFECTED.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. ORA_DM_PARTITION_NAME

## ORA_DM_PARTITION_NAME

Syntax

![Description of ora_dm_partition_name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/ora_dm_partition_name.gif)  
[Description of the illustration
ora_dm_partition_name.eps](img_text/ora_dm_partition_name.md)

mining_attribute_clause::=

![Description of mining_attribute_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/mining_attribute_clause.gif)  
[Description of the illustration
mining_attribute_clause.eps](img_text/mining_attribute_clause.md)

Purpose

`ORA_DM_PARTITION_NAME` is a single row function that works along with other
existing functions. This function returns the name of the partition associated
with the input row. When `ORA_DM_PARTITION_NAME` is used on a non-partitioned
model, the result is `NULL`.

The syntax of the `ORA_DM_PARTITION_NAME` function can use an optional
`GROUPING` hint when scoring a partitioned model. See [GROUPING
Hint](Comments.md#GUID-9693C230-2616-4123-A1ED-3C41E9566F7A).

mining_attribute_clause

The `mining_attribute_clause` identifies the column attributes to use as
predictors for scoring. When the function is invoked with the analytic syntax,
these predictors are also used for building the transient models. The
`mining_attribute_clause` behaves as described for the `PREDICTION` function.
See [mining_attribute_clause](PREDICTION.md#GUID-
DA66A1C3-BFB2-43A1-A3FF-93D4A3DAB9C6__MINING_ATTRIBUTE_CLAUSE-58BC0E25).

See Also:

  * [Oracle Machine Learning for SQL Userâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DMPRG004) for information about scoring 

  * [Oracle Machine Learning for SQL Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DMCON008) for information about clustering 

Note:

The following examples are excerpted from the Oracle Machine Learning for SQL
sample programs. For more information about the sample programs, see Appendix
A in [Oracle Machine Learning for SQL Userâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DMPRG714).

Example

    
    
    SELECT prediction(mymodel using *) pred, ora_dm_partition_name(mymodel USING *) pname FROM customers;


[← Previous](NVL2.md)

[Next →](ORA_DST_AFFECTED.md)
