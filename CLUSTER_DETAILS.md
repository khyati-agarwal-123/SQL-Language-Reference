[Previous](CHR.md) [Next](CLUSTER_DISTANCE.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. CLUSTER_DETAILS 

## CLUSTER_DETAILS

Syntax

cluster_details::=

![Description of cluster_details.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cluster_details.gif)  
[Description of the illustration
cluster_details.eps](img_text/cluster_details.md)

Analytic Syntax

cluster_details_analytic::=

![Description of cluster_details_analytic.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cluster_details_analytic.gif)  
[Description of the illustration
cluster_details_analytic.eps](img_text/cluster_details_analytic.md)

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

`CLUSTER_DETAILS` returns cluster details for each row in the selection. The
return value is an XML string that describes the attributes of the highest
probability cluster or the specified `cluster_id`.

topN

If you specify a value for `topN`, the function returns the `N` attributes
that most influence the cluster assignment (the score). If you do not specify
`topN`, the function returns the 5 most influential attributes.

DESC, ASC, or ABS

The returned attributes are ordered by weight. The weight of an attribute
expresses its positive or negative impact on cluster assignment. A positive
weight indicates an increased likelihood of assignment. A negative weight
indicates a decreased likelihood of assignment.

By default, `CLUSTER_DETAILS` returns the attributes with the highest positive
weights (`DESC`). If you specify `ASC`, the attributes with the highest
negative weights are returned. If you specify `ABS`, the attributes with the
greatest weights, whether negative or positive, are returned. The results are
ordered by absolute value from highest to lowest. Attributes with a zero
weight are not included in the output.

Syntax Choice

`CLUSTER_DETAILS` can score the data in one of two ways: It can apply a mining
model object to the data, or it can dynamically mine the data by executing an
analytic clause that builds and applies one or more transient mining models.
Choose Syntax or Analytic Syntax:

  * Syntax â Use the first syntax to score the data with a pre-defined model. Supply the name of a clustering model. 

  * Analytic Syntax â Use the analytic syntax to score the data without a pre-defined model. Include `INTO` `n`, where `n` is the number of clusters to compute, and `mining_analytic_clause`, which specifies if the data should be partitioned for multiple model builds. The `mining_analytic_clause` supports a `query_partition_clause` and an `order_by_clause`. (See [analytic_clause::=](Analytic-Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056__CJAFAAIA).) 

The syntax of the `CLUSTER_DETAILS` function can use an optional `GROUPING`
hint when scoring a partitioned model. See [GROUPING
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

This example lists the attributes that have the greatest impact (more that 20%
probability) on cluster assignment for customer ID 100955. The query invokes
the `CLUSTER_DETAILS` and `CLUSTER_SET` functions, which apply the clustering
model `em_sh_clus_sample`.

    
    
    SELECT S.cluster_id, probability prob,
           CLUSTER_DETAILS(em_sh_clus_sample, S.cluster_id, 5 USING T.*) det
    FROM
      (SELECT v.*, CLUSTER_SET(em_sh_clus_sample, NULL, 0.2 USING *) pset
        FROM mining_data_apply_v v
       WHERE cust_id = 100955) T,
      TABLE(T.pset) S
    ORDER BY 2 DESC;  
     
    CLUSTER_ID  PROB DET
    ---------- ----- ---------------------------------------------------------------------------------
            14 .6761 <Details algorithm="Expectation Maximization" cluster="14">
                     <Attribute name="AGE" actualValue="51" weight=".676" rank="1"/>
                     <Attribute name="HOME_THEATER_PACKAGE" actualValue="1" weight=".557" rank="2"/>
                     <Attribute name="FLAT_PANEL_MONITOR" actualValue="0" weight=".412" rank="3"/>
                     <Attribute name="Y_BOX_GAMES" actualValue="0" weight=".171" rank="4"/>
                     <Attribute name="BOOKKEEPING_APPLICATION" actualValue="1" weight="-.003"rank="5"/>
                     </Details>
     
             3 .3227 <Details algorithm="Expectation Maximization" cluster="3">
                     <Attribute name="YRS_RESIDENCE" actualValue="3" weight=".323" rank="1"/>
                     <Attribute name="BULK_PACK_DISKETTES" actualValue="1" weight=".265" rank="2"/>
                     <Attribute name="EDUCATION" actualValue="HS-grad" weight=".172" rank="3"/>
                     <Attribute name="AFFINITY_CARD" actualValue="0" weight=".125" rank="4"/>
                     <Attribute name="OCCUPATION" actualValue="Crafts" weight=".055" rank="5"/>
                     </Details>

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
    ------- --- -----------------------------------------------------------------------------------
     100001   5 <Details algorithm="K-Means Clustering" cluster="5">
                <Attribute name="FLAT_PANEL_MONITOR" actualValue="0" weight=".349" rank="1"/>
                <Attribute name="BULK_PACK_DISKETTES" actualValue="0" weight=".33" rank="2"/>
                <Attribute name="CUST_INCOME_LEVEL" actualValue="G: 130\,000 - 149\,999" weight=".291" 
                 rank="3"/>
                <Attribute name="HOME_THEATER_PACKAGE" actualValue="1" weight=".268" rank="4"/>
                <Attribute name="Y_BOX_GAMES" actualValue="0" weight=".179" rank="5"/>
                </Details>
    
     100002   6 <Details algorithm="K-Means Clustering" cluster="6">
                <Attribute name="CUST_GENDER" actualValue="F" weight=".945" rank="1"/>
                <Attribute name="CUST_MARITAL_STATUS" actualValue="NeverM" weight=".856" rank="2"/>
                <Attribute name="HOUSEHOLD_SIZE" actualValue="2" weight=".468" rank="3"/>
                <Attribute name="AFFINITY_CARD" actualValue="0" weight=".012" rank="4"/>
                <Attribute name="CUST_INCOME_LEVEL" actualValue="L: 300\,000 and above" weight=".009"
                 rank="5"/>
                </Details>
     
     100003   7 <Details algorithm="K-Means Clustering" cluster="7">
                <Attribute name="CUST_MARITAL_STATUS" actualValue="NeverM" weight=".862" rank="1"/>
                <Attribute name="HOUSEHOLD_SIZE" actualValue="2" weight=".423" rank="2"/>
                <Attribute name="HOME_THEATER_PACKAGE" actualValue="0" weight=".113" rank="3"/>
                <Attribute name="AFFINITY_CARD" actualValue="0" weight=".007" rank="4"/>
                <Attribute name="CUST_ID" actualValue="100003" weight=".006" rank="5"/>
                </Details>


[← Previous](CHR.md)

[Next →](CLUSTER_DISTANCE.md)
