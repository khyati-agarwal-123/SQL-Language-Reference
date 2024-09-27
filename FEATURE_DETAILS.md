[Previous](FEATURE_COMPARE.md) [Next](FEATURE_ID.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. FEATURE_DETAILS 

## FEATURE_DETAILS

Syntax

feature_details::=

![Description of feature_details.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/feature_details.gif)  
[Description of the illustration
feature_details.eps](img_text/feature_details.md)

Analytic Syntax

feature_details_analytic::=

![Description of feature_details_analytic.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/feature_details_analytic.gif)  
[Description of the illustration
feature_details_analytic.eps](img_text/feature_details_analytic.md)

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

`FEATURE_DETAILS` returns feature details for each row in the selection. The
return value is an XML string that describes the attributes of the highest
value feature or the specified `feature_id`.

topN

If you specify a value for `topN`, the function returns the `N` attributes
that most influence the feature value. If you do not specify `topN`, the
function returns the 5 most influential attributes.

DESC, ASC, or ABS

The returned attributes are ordered by weight. The weight of an attribute
expresses its positive or negative impact on the value of the feature. A
positive weight indicates a higher feature value. A negative weight indicates
a lower feature value.

By default, `FEATURE_DETAILS` returns the attributes with the highest positive
weight (`DESC`). If you specify `ASC`, the attributes with the highest
negative weight are returned. If you specify `ABS`, the attributes with the
greatest weight, whether negative or positive, are returned. The results are
ordered by absolute value from highest to lowest. Attributes with a zero
weight are not included in the output.

Syntax Choice

`FEATURE_DETAILS` can score the data in one of two ways: It can apply a mining
model object to the data, or it can dynamically mine the data by executing an
analytic clause that builds and applies one or more transient mining models.
Choose Syntax or Analytic Syntax:

  * Syntax â Use the first syntax to score the data with a pre-defined model. Supply the name of a feature extraction model. 

  * Analytic Syntax â Use the analytic syntax to score the data without a pre-defined model. Include `INTO` `n`, where `n` is the number of features to extract, and `mining_analytic_clause`, which specifies if the data should be partitioned for multiple model builds. The `mining_analytic_clause` supports a `query_partition_clause` and an `order_by_clause`. (See "[analytic_clause::=](Analytic-Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056__CJAFAAIA)".) 

The syntax of the `FEATURE_DETAILS` function can use an optional `GROUPING`
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

  * [Oracle Machine Learning for SQL Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DMCON010) for information about feature extraction. 

Note:

The following examples are excerpted from the Oracle Machine Learning for SQL
sample programs. For more information about the sample programs, see Appendix
A in [Oracle Machine Learning for SQL Userâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DMPRG714).

Example

This example uses the feature extraction model `nmf_sh_sample` to score the
data. The query returns the three features that best represent customer 100002
and the attributes that most affect those features.

    
    
    SELECT S.feature_id fid, value val,
           FEATURE_DETAILS(nmf_sh_sample, S.feature_id, 5 using T.*) det
       FROM
         (SELECT v.*, FEATURE_SET(nmf_sh_sample, 3 USING *) fset
             FROM mining_data_apply_v v
             WHERE cust_id = 100002) T,
       TABLE(T.fset) S
    ORDER BY 2 DESC;
     
     FID    VAL  DET
    ---- ------  ------------------------------------------------------------------------------------
       5  3.492  <Details algorithm="Non-Negative Matrix Factorization" feature="5">
                 <Attribute name="BULK_PACK_DISKETTES" actualValue="1" weight=".077" rank="1"/>
                 <Attribute name="OCCUPATION" actualValue="Prof." weight=".062" rank="2"/>
                 <Attribute name="BOOKKEEPING_APPLICATION" actualValue="1" weight=".001" rank="3"/>
                 <Attribute name="OS_DOC_SET_KANJI" actualValue="0" weight="0" rank="4"/>
                 <Attribute name="YRS_RESIDENCE" actualValue="4" weight="0" rank="5"/>
                 </Details>
       3  1.928  <Details algorithm="Non-Negative Matrix Factorization" feature="3">
                 <Attribute name="HOUSEHOLD_SIZE" actualValue="2" weight=".239" rank="1"/>
                 <Attribute name="CUST_INCOME_LEVEL" actualValue="L: 300\,000 and above" 
                  weight=".051" rank="2"/>
                 <Attribute name="FLAT_PANEL_MONITOR" actualValue="1" weight=".02" rank="3"/>
                 <Attribute name="HOME_THEATER_PACKAGE" actualValue="1" weight=".006" rank="4"/>
                 <Attribute name="AGE" actualValue="41" weight=".004" rank="5"/>
                 </Details>
       8   .816  <Details algorithm="Non-Negative Matrix Factorization" feature="8">
                 <Attribute name="EDUCATION" actualValue="Bach." weight=".211" rank="1"/>
                 <Attribute name="CUST_MARITAL_STATUS" actualValue="NeverM" weight=".143" rank="2"/>
                 <Attribute name="FLAT_PANEL_MONITOR" actualValue="1" weight=".137" rank="3"/>
                 <Attribute name="CUST_GENDER" actualValue="F" weight=".044" rank="4"/>
                 <Attribute name="BULK_PACK_DISKETTES" actualValue="1" weight=".032" rank="5"/>
                 </Details>

Analytic Example

This example dynamically maps customer attributes into six features and
returns the feature mapping for customer 100001.

    
    
    SELECT feature_id, value
      FROM (
         SELECT cust_id, feature_set(INTO 6 USING *) OVER () fset
            FROM mining_data_apply_v),
      TABLE (fset)
      WHERE cust_id = 100001
      ORDER BY feature_id;
     
    FEATURE_ID    VALUE
    ---------- --------
             1    2.670
             2     .000
             3    1.792
             4     .000
             5     .000
             6    3.379


[← Previous](FEATURE_COMPARE.md)

[Next →](FEATURE_ID.md)
