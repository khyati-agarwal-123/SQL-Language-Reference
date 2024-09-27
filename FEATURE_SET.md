[Previous](FEATURE_ID.md) [Next](FEATURE_VALUE.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. FEATURE_SET 

## FEATURE_SET

Syntax

feature_set::=

![Description of feature_set.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/feature_set.gif)  
[Description of the illustration feature_set.eps](img_text/feature_set.md)

Analytic Syntax

feature_set_analytic::=

![Description of feature_set_analytic.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/feature_set_analytic.gif)  
[Description of the illustration
feature_set_analytic.eps](img_text/feature_set_analytic.md)

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

`FEATURE_SET` returns a set of feature ID and feature value pairs for each row
in the selection. The return value is a varray of objects with field names
`FEATURE_ID` and `VALUE`. The data type of both fields is `NUMBER`.

topN and cutoff

You can specify `topN` and `cutoff` to limit the number of features returned
by the function. By default, both `topN` and `cutoff` are null and all
features are returned.

  * `topN` is the `N` highest value features. If multiple features have the `N`th value, then the function chooses one of them. 

  * `cutoff` is a value threshold. Only features that are greater than or equal to `cutoff` are returned. To filter by `cutoff` only, specify `NULL` for `topN`. 

To return up to `N` features that are greater than or equal to `cutoff`,
specify both `topN` and `cutoff`.

Syntax Choice

`FEATURE_SET` can score the data in one of two ways: It can apply a mining
model object to the data, or it can dynamically mine the data by executing an
analytic clause that builds and applies one or more transient mining models.
Choose Syntax or Analytic Syntax:

  * Syntax â Use the first syntax to score the data with a pre-defined model. Supply the name of a feature extraction model. 

  * Analytic Syntax â Use the analytic syntax to score the data without a pre-defined model. Include `INTO` `n`, where `n` is the number of features to extract, and `mining_analytic_clause`, which specifies if the data should be partitioned for multiple model builds. The `mining_analytic_clause` supports a `query_partition_clause` and an `order_by_clause`. (See "[analytic_clause::=](Analytic-Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056__CJAFAAIA)".) 

The syntax of the `FEATURE_SET` function can use an optional `GROUPING` hint
when scoring a partitioned model. See [GROUPING
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

The following example is excerpted from the Oracle Machine Learning for SQL
sample programs. For more information about the sample programs, see Appendix
A in [Oracle Machine Learning for SQL Userâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DMPRG714).

Example

This example lists the top features corresponding to a given customer record
and determines the top attributes for each feature (based on coefficient >
0.25).

    
    
    WITH
    feat_tab AS (
    SELECT F.feature_id fid,
           A.attribute_name attr,
           TO_CHAR(A.attribute_value) val,
           A.coefficient coeff
      FROM TABLE(DBMS_DATA_MINING.GET_MODEL_DETAILS_NMF('nmf_sh_sample')) F,
           TABLE(F.attribute_set) A
     WHERE A.coefficient > 0.25
    ),
    feat AS (
    SELECT fid,
           CAST(COLLECT(Featattr(attr, val, coeff))
             AS Featattrs) f_attrs
      FROM feat_tab
    GROUP BY fid
    ),
    cust_10_features AS (
    SELECT T.cust_id, S.feature_id, S.value
      FROM (SELECT cust_id, FEATURE_SET(nmf_sh_sample, 10 USING *) pset
              FROM nmf_sh_sample_apply_prepared
             WHERE cust_id = 100002) T,
           TABLE(T.pset) S
    )
    SELECT A.value, A.feature_id fid,
           B.attr, B.val, B.coeff
      FROM cust_10_features A,
           (SELECT T.fid, F.*
              FROM feat T,
                   TABLE(T.f_attrs) F) B
     WHERE A.feature_id = B.fid
    ORDER BY A.value DESC, A.feature_id ASC, coeff DESC, attr ASC, val ASC;
    
       VALUE  FID ATTR                      VAL                        COEFF
    -------- ---- ------------------------- ------------------------ -------
      6.8409    7 YRS_RESIDENCE                                       1.3879
      6.8409    7 BOOKKEEPING_APPLICATION                              .4388
      6.8409    7 CUST_GENDER               M                          .2956
      6.8409    7 COUNTRY_NAME              United States of America   .2848
      6.4975    3 YRS_RESIDENCE                                       1.2668
      6.4975    3 BOOKKEEPING_APPLICATION                              .3465
      6.4975    3 COUNTRY_NAME              United States of America   .2927
      6.4886    2 YRS_RESIDENCE                                       1.3285
      6.4886    2 CUST_GENDER               M                          .2819
      6.4886    2 PRINTER_SUPPLIES                                     .2704
      6.3953    4 YRS_RESIDENCE                                       1.2931
      5.9640    6 YRS_RESIDENCE                                       1.1585
      5.9640    6 HOME_THEATER_PACKAGE                                 .2576
      5.2424    5 YRS_RESIDENCE                                       1.0067
      2.4714    8 YRS_RESIDENCE                                        .3297
      2.3559    1 YRS_RESIDENCE                                        .2768
      2.3559    1 FLAT_PANEL_MONITOR                                   .2593


[← Previous](FEATURE_ID.md)

[Next →](FEATURE_VALUE.md)
