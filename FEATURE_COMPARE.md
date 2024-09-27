[Previous](EXTRACTVALUE.md) [Next](FEATURE_DETAILS.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. FEATURE_COMPARE

## FEATURE_COMPARE

Syntax

feature_compare::=

![Description of feature_compare.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/feature_compare.gif)  
[Description of the illustration
feature_compare.eps](img_text/feature_compare.md)

mining_attribute_clause::=

![Description of mining_attribute_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/mining_attribute_clause.gif)  
[Description of the illustration
mining_attribute_clause.eps](img_text/mining_attribute_clause.md)

Purpose

The `FEATURE_COMPARE` function uses a Feature Extraction model to compare two
different documents, including short ones such as keyword phrases or two
attribute lists, for similarity or dissimilarity. The `FEATURE_COMPARE`
function can be used with Feature Extraction algorithms such as Singular Value
Decomposition (SVD), Principal Component Analysis PCA), Non-Negative Matrix
Factorization (NMF), and Explicit Semantic Analysis (ESA). This function is
applicable not only to documents, but also to numeric and categorical data.

The input to the `FEATURE_COMPARE` function is a single feature model built
using the Feature Extraction algorithms of Oracle Machine Learning for SQL,
such as NMF, SVD, and ESA. The double `USING` clause provides a mechanism to
compare two different documents or constant keyword phrases, or any
combination of the two, for similarity or dissimilarity using the extracted
features in the model.

The syntax of the `FEATURE_COMPARE` function can use an optional `GROUPING`
hint when scoring a partitioned model. See [GROUPING
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

Examples

An ESA model is built against a 2005 Wiki dataset rendering over 200,000
features. The documents are mined as text and the document titles are
considered as the Feature IDs.

The examples show the `FEATURE_COMPARE` function with the ESA algorithm, which
compares a similar set of texts and then a dissimilar set of texts.

Similar texts

    
    
    SELECT 1-FEATURE_COMPARE(esa_wiki_mod USING 'There are several PGA tour golfers from South Africa' text AND USING 'Nick Price won the 2002 Mastercard Colonial Open' text) similarity FROM DUAL;
    
    SIMILARITY
    ----------
          .258

The output metric shows the results of a distance calculation. Therefore, a
smaller number represents more similar texts. So 1 minus the distance in the
queries represents a document similarity metric.

Dissimilar texts

    
    
    SELECT 1-FEATURE_COMPARE(esa_wiki_mod USING 'There are several PGA tour golfers from South Africa' text AND USING 'John Elway played quarterback for the Denver Broncos' text) similarity FROM DUAL;
    
    SIMILARITY
    ----------
          .007
    
    


[← Previous](EXTRACTVALUE.md)

[Next →](FEATURE_DETAILS.md)
