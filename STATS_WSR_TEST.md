[Previous](STATS_T_TEST_.md) [Next](STDDEV.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. STATS_WSR_TEST 

## STATS_WSR_TEST

Syntax

![Description of stats_wsr_test.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/stats_wsr_test.gif)  
[Description of the illustration
stats_wsr_test.eps](img_text/stats_wsr_test.md)

Purpose

`STATS_WSR_TEST` is a Wilcoxon Signed Ranks test of paired samples to
determine whether the median of the differences between the samples is
significantly different from zero. The absolute values of the differences are
ordered and assigned ranks. Then the null hypothesis states that the sum of
the ranks of the positive differences is equal to the sum of the ranks of the
negative differences.

This function takes two required arguments: `expr1` and `expr2` are the two
samples being analyzed. The optional third argument lets you specify the
meaning of the `NUMBER` value returned by this function, as shown in [Table
7-10](STATS_WSR_TEST.md#GUID-80A8A9A9-7CD9-4358-B628-6D67BD42BA5B__G1514203
"The first column lists the values you can specify for the argument of the
function and the second column explains the return value meanings."). For this
argument, you can specify a text literal, or a bind variable or expression
that evaluates to a constant character value. If you omit the third argument,
then the default is `'TWO_SIDED_SIG'`.

Table 7-10 STATS_WSR_TEST_* Return Values

Argument | Return Value Meaning  
---|---  
`'STATISTIC'` |  The observed value of Z  
`'ONE_SIDED_SIG'` |  One-tailed significance of Z  
`'TWO_SIDED_SIG'` |  Two-tailed significance of Z  
  
One-sided significance is always with respect to the upper tail. The high
value (the value whose rejection region is the upper tail) is `expr1`.


[← Previous](STATS_T_TEST_.md)

[Next →](STDDEV.md)
