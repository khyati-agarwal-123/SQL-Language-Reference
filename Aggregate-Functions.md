[Previous](About-SQL-Functions.md) [Next](Analytic-Functions.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. Aggregate Functions 

## Aggregate Functions

Aggregate functions return a single result row based on groups of rows, rather
than on single rows. Aggregate functions can appear in select lists and in
`ORDER` `BY` and `HAVING` clauses. They are commonly used with the `GROUP`
`BY` clause in a `SELECT` statement, where Oracle Database divides the rows of
a queried table or view into groups. In a query containing a `GROUP` `BY`
clause, the elements of the select list can be aggregate functions, `GROUP`
`BY` expressions, constants, or expressions involving one of these. Oracle
applies the aggregate functions to each group of rows and returns a single
result row for each group.

If you omit the `GROUP` `BY` clause, then Oracle applies aggregate functions
in the select list to all the rows in the queried table or view. You use
aggregate functions in the `HAVING` clause to eliminate groups from the output
based on the results of the aggregate functions, rather than on the values of
the individual rows of the queried table or view.

See Also:

  * [Using the GROUP BY Clause: Examples](SELECT.md#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6__I2066419) and the [HAVING Clause](SELECT.md#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6__I2078943) for more information on the `GROUP` `BY` clause and `HAVING` clauses in queries and subqueries 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation determination rules for expressions in the `ORDER` `BY` clause of an aggregate function 

Many (but not all) aggregate functions that take a single argument accept
these clauses:

  * `DISTINCT` and `UNIQUE`, which are synonymous, cause an aggregate function to consider only distinct values of the argument expression. The syntax diagrams for aggregate functions in this chapter use the keyword `DISTINCT` for simplicity. 

  * `ALL` causes an aggregate function to consider all values, including all duplicates. 

For example, the `DISTINCT` average of 1, 1, 1, and 3 is 2. The `ALL` average
is 1.5. If you specify neither, then the default is `ALL`.

Some aggregate functions allow the `windowing_clause`, which is part of the
syntax of analytic functions. Refer to [windowing_clause](Analytic-
Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056__I97640) for
information about this clause.

All aggregate functions except `COUNT`(*), `GROUPING`, and `GROUPING_ID`
ignore nulls. You can use the `NVL` function in the argument to an aggregate
function to substitute a value for a null. `COUNT` and `REGR_COUNT` never
return null, but return either a number or zero. For all the remaining
aggregate functions, if the data set contains no rows, or contains only rows
with nulls as arguments to the aggregate function, then the function returns
null.

The aggregate functions `MIN`, `MAX`, `SUM`, `AVG`, `COUNT`, `VARIANCE`, and
`STDDEV`, when followed by the `KEEP` keyword, can be used in conjunction with
the `FIRST` or `LAST` function to operate on a set of values from a set of
rows that rank as the `FIRST` or `LAST` with respect to a given sorting
specification. Refer to
[FIRST](FIRST.md#GUID-85AB9246-0E0A-44A1-A7E6-4E57502E9238) for more
information.

You can nest aggregate functions. For example, the following example
calculates the average of the maximum salaries of all the departments in the
sample schema `hr`:

    
    
    SELECT AVG(MAX(salary))
      FROM employees
      GROUP BY department_id;
    
    AVG(MAX(SALARY))
    ----------------
          10926.3333
    

This calculation evaluates the inner aggregate (`MAX`(`salary`)) for each
group defined by the `GROUP` `BY` clause (`department_id`), and aggregates the
results again.

  * [ANY_VALUE](ANY_VALUE.md#GUID-A3C47D5E-B145-40B2-93D2-CA3BA65C2D81)
  * [APPROX_COUNT](APPROX_COUNT.md#GUID-7D07E04A-3F9A-425E-BADE-EDA9C6162E9C)
  * [APPROX_COUNT_DISTINCT](APPROX_COUNT_DISTINCT.md#GUID-50055A05-0187-4481-AFE5-2414F7227713)
  * [APPROX_COUNT_DISTINCT_AGG](APPROX_COUNT_DISTINCT_AGG.md#GUID-EEDA9388-A066-422A-B5C0-639A3076A10B)
  * [APPROX_COUNT_DISTINCT_DETAIL](APPROX_COUNT_DISTINCT_DETAIL.md#GUID-8FBD2881-743D-425E-A104-472A720DEF50)
  * [APPROX_MEDIAN](APPROX_MEDIAN.md#GUID-F6A11DF2-121A-4057-9D0B-BF1A221B5622)
  * [APPROX_PERCENTILE](APPROX_PERCENTILE.md#GUID-70D54091-EE2F-4283-A10B-1AB5A1242FE2)
  * [APPROX_PERCENTILE_AGG](APPROX_PERCENTILE_AGG.md#GUID-72A1DAB0-4A3E-42BF-9E20-92273AD62E11)
  * [APPROX_PERCENTILE_DETAIL](APPROX_PERCENTILE_DETAIL.md#GUID-F9A0B9B5-671F-43CA-9FA7-69A2DD174F54)
  * [APPROX_RANK](APPROX_RANK.md#GUID-4F20978C-3188-4225-863D-0F7A25FD78FD)
  * [APPROX_SUM](APPROX_SUM.md#GUID-AC2A72A7-24E5-4FB8-B012-BD35CB560D6B)
  * [AVG](AVG.md#GUID-B64BCBF1-DAA0-4D88-9821-2C4D3FDE5E4A)
  * [BIT_AND_AGG](BIT_AND_AGG.md#GUID-82497098-6D77-48D3-89EF-C1041BF8A258)
  * [BIT_OR_AGG](BIT_OR_AGG.md#GUID-18B0E3CB-1C90-4625-8E36-B422FA4E04A8)
  * [BIT_XOR_AGG](BIT_XOR_AGG.md#GUID-1563FB7E-9CC9-4D03-859E-BE336AF01F1D)
  * [BOOLEAN_AND_AGG](boolean_and_agg.md#GUID-AF3C1A26-C7A1-4BD2-B15C-86B761D4D8D9)
  * [BOOLEAN_OR_AGG](boolean_or_agg.md#GUID-C3E187DE-BD26-4440-B0AD-51342FFA4775)
  * [CHECKSUM](checksum.md#GUID-3F55C5DF-F23A-4B2F-BC6F-E03B34B78BA8)
  * [COLLECT](COLLECT.md#GUID-A0A74602-2A97-449B-A3EC-847D38D3DA90)
  * [CORR](CORR.md#GUID-E73AF5E2-38A4-436A-955C-5122C079F49C)
  * [CORR_*](CORR_A.md#GUID-B2DED35A-2ECE-4DF0-BDA4-28F28B7BCA23)
  * [COUNT](COUNT.md#GUID-AEF08B79-024D-4E3A-B362-9715FB011776)
  * [COVAR_POP](COVAR_POP.md#GUID-D728D05F-D2E3-405C-986F-088B8353553A)
  * [COVAR_SAMP](COVAR_SAMP.md#GUID-7850B9E1-83A4-41CB-8F17-DCD2E2A70C95)
  * [CUME_DIST](CUME_DIST.md#GUID-B12C577C-A63C-4D19-8E18-FCCBBFBF8278)
  * [DENSE_RANK](DENSE_RANK.md#GUID-BB66F574-09DF-4594-87A4-ABD83E8DC3FE)
  * [EVERY](every.md#GUID-C34D8A50-3050-4F32-941A-8C2512DEC62D)
  * [FIRST](FIRST.md#GUID-85AB9246-0E0A-44A1-A7E6-4E57502E9238)
  * [GROUP_ID](GROUP_ID.md#GUID-3A5A9C15-1B67-4FD7-AC41-EE8349B2E834)
  * [GROUPING](GROUPING.md#GUID-82E6084A-0BDF-4587-A40E-36899783F073)
  * [GROUPING_ID](GROUPING_ID.md#GUID-E20A5B8E-73B6-42FD-8AFB-DD3CD6D6DC61)
  * [JSON_ARRAYAGG](JSON_ARRAYAGG.md#GUID-6D56077D-78DE-4CC0-9498-225DDC42E054)
  * [JSON_OBJECTAGG](JSON_OBJECTAGG.md#GUID-09422D4A-936C-4D38-9991-C64101283D98)
  * [KURTOSIS_POP](KURTOSIS_POP.md#GUID-F820DFF7-B758-460E-AECC-053915069B9F)
  * [KURTOSIS_SAMP](KURTOSIS_SAMP.md#GUID-487DE503-A015-415F-B6CD-F9D095B91178)
  * [LAST](LAST.md#GUID-4E16BC0E-D3B8-4BA4-8F97-3A08891A85CC)
  * [LISTAGG](LISTAGG.md#GUID-B6E50D8E-F467-425B-9436-F7F8BF38D466)
  * [MAX](MAX.md#GUID-E5372020-A6DA-44BF-93BE-DA8C3F74CD01)
  * [MEDIAN](MEDIAN.md#GUID-DE15705A-AC18-4416-8487-B9E1D70CE01A)
  * [MIN](MIN.md#GUID-F7F04E18-1AD8-4D15-9491-4622AD847A74)
  * [PERCENT_RANK](PERCENT_RANK.md#GUID-66A868F5-9EBA-482A-BF8C-09300B9EE165)
  * [PERCENTILE_CONT](PERCENTILE_CONT.md#GUID-CA259452-A565-41B3-A4F4-DD74B66CEDE0)
  * [PERCENTILE_DISC](PERCENTILE_DISC.md#GUID-7C34FDDA-C241-474F-8C5C-50CC0182E005)
  * [RANK](RANK.md#GUID-0950BD34-C994-41DA-A8F9-34B3FE53BBBA)
  * [REGR_ (Linear Regression) Functions](REGR_-Linear-Regression-Functions.md#GUID-A675B68F-2A88-4843-BE2C-FCDE9C65F9A9)
  * [SKEWNESS_POP](SKEWNESS_POP.md#GUID-DF34158F-B681-4933-BA27-0A3885A9F43C)
  * [SKEWNESS_SAMP](SKEWNESS_SAMP.md#GUID-E71D9AEC-0AAA-4A6C-BF70-29EE9AD8F7EC)
  * [STATS_BINOMIAL_TEST](STATS_BINOMIAL_TEST.md#GUID-3DDCDC0C-0DB2-479F-A6EB-E9FC0063ABF4)
  * [STATS_CROSSTAB](STATS_CROSSTAB.md#GUID-AA0958AE-FF56-4970-B880-23426E0B7E6D)
  * [STATS_F_TEST](STATS_F_TEST.md#GUID-9E2A91FC-5BB3-449A-810C-DA6CB52B56ED)
  * [STATS_KS_TEST](STATS_KS_TEST.md#GUID-ADE2ACB3-C852-499F-8892-E4AA101EC80D)
  * [STATS_MODE](STATS_MODE.md#GUID-10BDACE0-C435-4E3F-BC50-FD1A41C0F508)
  * [STATS_MW_TEST](STATS_MW_TEST.md#GUID-77AF4F10-D4DC-45A9-94E8-F4F648F81222)
  * [STATS_ONE_WAY_ANOVA](STATS_ONE_WAY_ANOVA.md#GUID-CC614CE5-56CB-4A54-8571-6FEAD2D2E75F)
  * [STATS_T_TEST_*](STATS_T_TEST_.md#GUID-B570D6F6-E4D7-4033-AC83-7E76F2E9CC2A)
  * [STATS_WSR_TEST](STATS_WSR_TEST.md#GUID-80A8A9A9-7CD9-4358-B628-6D67BD42BA5B)
  * [STDDEV](STDDEV.md#GUID-CA0C3B1F-1A4C-4CFB-ADAB-D90216C4E099)
  * [STDDEV_POP](STDDEV_POP.md#GUID-4F804DE5-7E20-4E08-A1BA-32DBB167B34B)
  * [STDDEV_SAMP](STDDEV_SAMP.md#GUID-7B2A708E-E73A-4CFE-978E-3F9C4BD37467)
  * [SUM](SUM.md#GUID-5610BE2C-CFE5-446F-A1F7-B924B5663220)
  * [SYS_OP_ZONE_ID](SYS_OP_ZONE_ID.md#GUID-947900CE-F4E0-43B5-B30C-4FDDA3913F17)
  * [SYS_XMLAGG](SYS_XMLAGG.md#GUID-BEDD241D-360A-46A2-AEBF-C8B70E465D75)
  * [TO_APPROX_COUNT_DISTINCT](TO_APPROX_COUNT_DISTINCT.md#GUID-42A18FFB-C992-44A0-AC3E-F4BBF005846F)
  * [TO_APPROX_PERCENTILE](TO_APPROX_PERCENTILE.md#GUID-463702B2-9199-41ED-AE03-865CABAD3E23)
  * [VAR_POP](VAR_POP.md#GUID-B62FB4A4-BD1F-47B0-B412-31A98B70C2E4)
  * [VAR_SAMP](VAR_SAMP.md#GUID-314D5831-0E26-4ABF-9F46-35F78F97DA52)
  * [VARIANCE](VARIANCE.md#GUID-EC33717A-2509-402D-B3BB-7EECB2E4ED8B)
  * [XMLAGG](XMLAGG.md#GUID-BCD1D755-5E26-4F73-BA22-521C30D275DA)


[← Previous](About-SQL-Functions.md)

[Next →](Analytic-Functions.md)
