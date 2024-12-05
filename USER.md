[Previous](UPPER.html) [Next](USERENV.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)
  2. [Functions](Functions.html)
  3. USER 



## USER 

Syntax

![Description of user.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/user.gif)[Description of the illustration user.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/user.html)

Purpose

`USER` returns the name of the session user (the user who logged on). This may change during the duration of a database session as Real Application Security sessions are attached or detached. If a Real Application Security session is currently attached to the database session, then it returns user `XS$NULL`. 

This function returns a `VARCHAR2` value. 

Oracle Database compares values of this function with blank-padded comparison semantics.

In a distributed SQL statement, the `UID` and `USER` functions together identify the user on your local database. You cannot use these functions in the condition of a `CHECK` constraint. 

See Also:

Appendix C in [Oracle Database Globalization Support Guide](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of `USER`

Examples

The following example returns the session user and the user's UID:
    
    
    SELECT USER, UID FROM DUAL;

[← Previous](UPPER.md)

[Next →](USERENV.md)
