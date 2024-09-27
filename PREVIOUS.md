[Previous](PRESENTV.md) [Next](RANK.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. PREVIOUS 

## PREVIOUS

Syntax

![Description of previous.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/previous.gif)  
[Description of the illustration previous.eps](img_text/previous.md)

Purpose

The `PREVIOUS` function can be used only in the `model_clause` of the `SELECT`
statement and then only in the `ITERATE` ... [ `UNTIL` `]` clause of the
`model_rules_clause`. It returns the value of `cell_reference` at the
beginning of each iteration.

See Also:

  * [model_clause](SELECT.md#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6__I2172805) and "[Model Expressions](Model-Expressions.md#GUID-83D3FD56-8346-4D3F-A49E-5FE41FE19257)" for the syntax and semantics 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the return value of `PREVIOUS` when it is a character value 

Examples

The following example repeats the rules, up to 1000 times, until the
difference between the values of `cur_val` at the beginning and at the end of
an iteration is less than one:

    
    
    SELECT dim_col, cur_val, num_of_iterations
      FROM (SELECT 1 AS dim_col, 10 AS cur_val FROM dual)
      MODEL
        DIMENSION BY (dim_col)
        MEASURES (cur_val, 0 num_of_iterations)
        IGNORE NAV
        UNIQUE DIMENSION
        RULES ITERATE (1000) UNTIL (PREVIOUS(cur_val[1]) - cur_val[1] < 1)
        (
          cur_val[1] = cur_val[1]/2,
          num_of_iterations[1] = num_of_iterations[1] + 1
        );
    
       DIM_COL    CUR_VAL NUM_OF_ITERATIONS
    ---------- ---------- -----------------
             1       .625                 4


[← Previous](PRESENTV.md)

[Next →](RANK.md)
