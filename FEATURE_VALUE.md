##  FEATURE_VALUE {#GUID-EC0E44D0-BE01-49F8-9E5A-72B500119877} 

Syntax 

*feature_value* ::= 

![Description of feature_value.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/feature_value.gif)[ Description of the illustration feature_value.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/feature_value.md)

Analytic Syntax 

*feature_value_analytic* ::= 

![Description of feature_value_analytic.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/feature_value_analytic.gif)[ Description of the illustration feature_value_analytic.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/feature_value_analytic.md)

*mining_attribute_clause* ::= 

![Description of mining_attribute_clause.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/mining_attribute_clause.gif)[ Description of the illustration mining_attribute_clause.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/mining_attribute_clause.md)

*mining_analytic_clause* ::= 

![Description of mining_analytic_clause.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/mining_analytic_clause.gif)[ Description of the illustration mining_analytic_clause.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/mining_analytic_clause.md)

> **note:** See Also: 

" [ Analytic Functions ](Analytic-Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056) "  for information on the syntax, semantics, and restrictions of *mining_analytic_clause* 

Purpose 

` FEATURE_VALUE ` returns a feature value for each row in the selection. The value refers to the highest value feature or to the specified *feature_id* . The feature value is returned as ` BINARY_DOUBLE ` . 

Syntax Choice 

` FEATURE_VALUE ` can score the data in one of two ways: It can apply a mining model object to the data, or it can dynamically mine the data by executing an analytic clause that builds and applies one or more transient mining models. Choose  Syntax  or  Analytic Syntax  : 

  * Syntax  — Use the first syntax to score the data with a pre-defined model. Supply the name of a feature extraction model. 

  * Analytic Syntax  — Use the analytic syntax to score the data without a pre-defined model. Include ` INTO ` *n* , where *n* is the number of features to extract, and *mining_analytic_clause* , which specifies if the data should be partitioned for multiple model builds. The *mining_analytic_clause* supports a *query_partition_clause* and an *order_by_clause* . (See  " [ analytic_clause::= ](Analytic-Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056__CJAFAAIA) "  .) 




The syntax of the ` FEATURE_VALUE ` function can use an optional ` GROUPING ` hint when scoring a partitioned model. See [ GROUPING Hint ](Comments.md#GUID-9693C230-2616-4123-A1ED-3C41E9566F7A) . 

mining_attribute_clause 

*mining_attribute_clause* identifies the column attributes to use as predictors for scoring. When the function is invoked with the analytic syntax, this data is also used for building the transient models. The *mining_attribute_clause* behaves as described for the ` PREDICTION ` function. (See  " [ mining_attribute_clause::= ](PREDICTION.md#GUID-DA66A1C3-BFB2-43A1-A3FF-93D4A3DAB9C6__CJAIGCFC) "  .) 

> **note:** See Also: 

  * [ *Oracle Machine Learning for SQL User’s Guide*  ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DMPRG004) for information about scoring. 

  * [ *Oracle Machine Learning for SQL Concepts*  ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DMCON010) for information about feature extraction. 




> **note:** 

The following example is excerpted from the Oracle Machine Learning for SQL sample programs. For more information about the sample programs, see Appendix A in [ *Oracle Machine Learning for SQL User’s Guide*  ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DMPRG714) . 

Example 

The following example lists the customers that correspond to feature 3, ordered by match quality. 
    
    
    ```
    SELECT *
      FROM (SELECT cust_id, FEATURE_VALUE(nmf_sh_sample, 3 USING *) match_quality
              FROM nmf_sh_sample_apply_prepared
              ORDER BY match_quality DESC)
      WHERE ROWNUM < 11;
    
       CUST_ID MATCH_QUALITY
    ---------- -------------
        100210    19.4101627
        100962    15.2482251
        101151    14.5685197
        101499    14.4186292
        100363    14.4037396
        100372    14.3335148
        100982    14.1716545
        101039    14.1079914
        100759    14.0913761
        100953    14.0799737
    ```
