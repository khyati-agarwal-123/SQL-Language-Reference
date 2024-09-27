[Previous](CLUSTER_DISTANCE.md) [Next](CLUSTER_PROBABILITY.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. CLUSTER_ID 

## CLUSTER_ID

Syntax

cluster_id::=

![Description of cluster_id.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cluster_id.gif)  
[Description of the illustration cluster_id.eps](img_text/cluster_id.md)

Analytic Syntax

cluster_id_analytic::=

![Description of cluster_id_analytic.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cluster_id_analytic.gif)  
[Description of the illustration
cluster_id_analytic.eps](img_text/cluster_id_analytic.md)

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

`CLUSTER_ID` returns the identifier of the highest probability cluster for
each row in the selection. The cluster identifier is returned as an Oracle
`NUMBER`.

Syntax Choice

`CLUSTER_ID` can score the data in one of two ways: It can apply a mining
model object to the data, or it can dynamically mine the data by executing an
analytic clause that builds and applies one or more transient mining models.
Choose Syntax or Analytic Syntax:

  * Syntax â Use the first syntax to score the data with a pre-defined model. Supply the name of a clustering model. 

  * Analytic Syntax â Use the analytic syntax to score the data without a pre-defined model. Include `INTO` `n`, where `n` is the number of clusters to compute, and `mining_analytic_clause`, which specifies if the data should be partitioned for multiple model builds. The `mining_analytic_clause` supports a `query_partition_clause` and an `order_by_clause`. (See [analytic_clause::=](Analytic-Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056__CJAFAAIA).) 

The syntax of the `CLUSTER_ID` function can use an optional `GROUPING` hint
when scoring a partitioned model. See [GROUPING
Hint](Comments.md#GUID-9693C230-2616-4123-A1ED-3C41E9566F7A).

mining_attribute_clause

`mining_attribute_clause` identifies the column attributes to use as
predictors for scoring. When the function is invoked with the analytic syntax,
these predictors are also used for building the transient models. The
`mining_attribute_clause` behaves as described for the `PREDICTION` function.
(See [mining_attribute_clause::=](PREDICTION.md#GUID-
DA66A1C3-BFB2-43A1-A3FF-93D4A3DAB9C6__CJAIGCFC).)

See Also:

  * [Oracle Machine Learning for SQL Userâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DMPRG004) for information about scoring. 

  * [Oracle Machine Learning for SQL Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DMCON008) for information about clustering. 

Note:

The following examples are excerpted from the Oracle Machine Learning for SQL
sample programs. For more information about the sample programs, see Appendix
A in [Oracle Machine Learning for SQL Userâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DMPRG714).

Example

The following example lists the clusters into which the customers in
`mining_data_apply_v` have been grouped.

    
    
    SELECT CLUSTER_ID(km_sh_clus_sample USING *) AS clus, COUNT(*) AS cnt 
      FROM mining_data_apply_v
      GROUP BY CLUSTER_ID(km_sh_clus_sample USING *)
      ORDER BY cnt DESC;
    
          CLUS        CNT
    ---------- ----------
             2        580
            10        216
             6        186
             8        115
            19        110
            12        101
            18         81
            16         39
            17         38
            14         34

Analytic Example

This example divides the customer database into four segments based on common
characteristics. The clustering functions compute the clusters and return the
score without a predefined clustering model.

    
    
    SELECT * FROM (
         SELECT cust_id,
              CLUSTER_ID(INTO 4 USING *) OVER () cls,
              CLUSTER_DETAILS(INTO 4 USING *) OVER () cls_details
         FROM mining_data_apply_v)
    WHERE cust_id <= 100003
    ORDER BY 1; 
     
    CUST_ID CLS CLS_DETAILS
    ------- --- -----------------------------------------------------------------------------
     100001   5 <Details algorithm="K-Means Clustering" cluster="5">
                <Attribute name="FLAT_PANEL_MONITOR" actualValue="0" weight=".349" rank="1"/>
                <Attribute name="BULK_PACK_DISKETTES" actualValue="0" weight=".33" rank="2"/>
                <Attribute name="CUST_INCOME_LEVEL" actualValue="G: 130\,000 - 149\,999"
                   weight=".291" rank="3"/>
                <Attribute name="HOME_THEATER_PACKAGE" actualValue="1" weight=".268" rank="4"/>
                <Attribute name="Y_BOX_GAMES" actualValue="0" weight=".179" rank="5"/>
                </Details>
    
     100002   6 <Details algorithm="K-Means Clustering" cluster="6">
                <Attribute name="CUST_GENDER" actualValue="F" weight=".945" rank="1"/>
                <Attribute name="CUST_MARITAL_STATUS" actualValue="NeverM" weight=".856" rank="2"/>
                <Attribute name="HOUSEHOLD_SIZE" actualValue="2" weight=".468" rank="3"/>
                <Attribute name="AFFINITY_CARD" actualValue="0" weight=".012" rank="4"/>
                <Attribute name="CUST_INCOME_LEVEL" actualValue="L: 300\,000 and above" 
                   weight=".009" rank="5"/>
                </Details>
     
     100003   7 <Details algorithm="K-Means Clustering" cluster="7">
                <Attribute name="CUST_MARITAL_STATUS" actualValue="NeverM" weight=".862" rank="1"/>
                <Attribute name="HOUSEHOLD_SIZE" actualValue="2" weight=".423" rank="2"/>
                <Attribute name="HOME_THEATER_PACKAGE" actualValue="0" weight=".113" rank="3"/>
                <Attribute name="AFFINITY_CARD" actualValue="0" weight=".007" rank="4"/>
                <Attribute name="CUST_ID" actualValue="100003" weight=".006" rank="5"/>
                </Details>


[← Previous](CLUSTER_DISTANCE.md)

[Next →](CLUSTER_PROBABILITY.md)
