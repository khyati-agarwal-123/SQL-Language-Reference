##  SKEWNESS_SAMP {#GUID-E71D9AEC-0AAA-4A6C-BF70-29EE9AD8F7EC} 

Syntax 

![Description of skewness_samp.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/skewness_samp.gif)[ Description of the illustration skewness_samp.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/skewness_samp.md)

Purpose 

` SKEWNESS_SAMP ` is an aggregate function that is primarily used to determine symmetry in a given distribution. 

NULL values in ` expr ` are ignored. 

Returns NULL if all rows in the group have NULL ` expr ` values. 

Returns 0 if there are one or two rows in ` expr ` . 

For a given set of values, the result of population skewness ( ` SKEWNESS_POP ` ) and sample skewness ( ` SKEWNESS_SAMP ` ) are always deterministic. However, the values of ` SKEWNESS_POP ` and ` SKEWNESS_SAMP ` differ. As the number of values in the data set increases, the difference between the computed values of ` SKEWNESS_SAMP ` and ` SKEWNESS_POP ` decreases. 
