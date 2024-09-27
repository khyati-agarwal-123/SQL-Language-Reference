[Previous](ISO-Standards.md) [Next](Oracle-Support-for-Optional-Features-of-
SQLFoundation2011.md) JavaScript must be enabled to correctly display this
content

  1. [SQL Language Reference ](index.md)
  2. [ Oracle and Standard SQL](Oracle-and-Standard-SQL.md)
  3. Oracle Compliance to Core SQL

## Oracle Compliance to Core SQL

The ANSI and ISO SQL standards require conformance claims to state the type of
conformance and the implemented facilities. The minimum claim of conformance
is called Core SQL and is defined in Part 2, SQL/Foundation, and Part 11,
SQL/Schemata, of the standard. The following products provide full or partial
conformance with Core SQL as described in the tables that follow:

  * Oracle Database server, release 12.2

  * OTT (Oracle Type Translator), release 12.2

  * Pro*C/C++, release 12.2

  * Pro*COBOL, release 12.2

The SQL standards conformance features can be used either as a guide to
portability, or as a guide to functionality. From the standpoint of
portability, the user is interested in conformance to both the precise syntax
and semantics of the standard feature. From the standpoint of functionality,
the user is less concerned about the precise syntax and more concerned with
issues of semantics. The tables in this appendix use the following terms
regarding support for standard syntax and semantics:

  * Full Support: The feature is supported with standard syntax and semantics.

  * Partial Support: Some, but not all, of the standard syntax is supported; whatever is supported has standard semantics.

  * Enhanced Support: The standard semantics is supported, as well as additional functionality.

  * Equivalent Support: The standard semantics is supported using non-standard syntax.

  * Similar Support: Neither the standard's syntax nor semantics are supported precisely, but similar functionality is provided.

Oracle's support for the features of Core SQL is listed in [Table C-1](Oracle-
Compliance-To-Core-
SQL2011.md#GUID-D372D906-805B-49B8-824A-D4697B05B7F8__G14847 "Column 1
contains the SQL:2008 feature identifier and its descrption and column 2
describes the Oracle Database support of the feature."):

Table C-1 Oracle Support of Core SQL Features

Feature ID |  Feature Support  
---|---  
E011, Numeric data types |  Oracle fully supports this feature.  
E021, Character data types |  Oracle fully supports these subfeatures:

  * E021-01, `CHARACTER` data type 
  * E021-07, Character concatenation
  * E021-08, `UPPER` and `LOWER` functions 
  * E021-09, `TRIM` function 
  * E021-10, Implicit casting among character data types

Oracle partially supports these subfeatures:

  * E021-02, `CHARACTER` `VARYING` data type (Oracle does not distinguish a zero-length `VARCHAR` string from `NULL`) 
  * E021-03, Character literals (Oracle regards the zero-length literal '' as being null)
  * E021-12, Character comparison (Oracle's rules for padding the shorter of two strings to be compared differs from the standard)

Oracle has equivalent functionality for these subfeatures:

  * E021-04, `CHARACTER_LENGTH` function: use `LENGTH` function instead 
  * E021-05, `OCTET_LENGTH` function: use `LENGTHB` function instead 
  * E021-06, `SUBSTRING` function: use `SUBSTR` function instead 
  * E021-11, `POSITION` function: use `INSTR` function instead 

  
E031, Identifiers |  Oracle supports this feature, with the following exceptions:

  * Oracle does not support the escape sequence to permit a double quote within a quoted identifier
  * A non-quoted identifier may not be equivalent to an Oracle reserved word (the list of Oracle reserved words differs from the standard's list)
  * A column name may not be `ROWID`, even as a quoted identifier 

Oracle extends this feature as follows:

  * An identifier may be up to 128 characters long
  * A non-quoted identifier may have dollar sign ($) or pound sign (#)

  
E051, Basic query specification |  Oracle fully supports the following subfeatures:

  * E051-01, `SELECT` `DISTINCT`
  * E051-02, `GROUP` `BY` clause 
  * E051-04, `GROUP` `BY` can contain columns not in `SELECT` list 
  * E051-05, `SELECT` list items can be renamed 
  * E051-06, `HAVING` clause 
  * E051-07, Qualified * in `SELECT` list 

Oracle partially supports the following subfeatures:

  * E051-08, Correlation names in `FROM` clause (Oracle supports correlation names, but not the optional `AS` keyword) 

Oracle has equivalent functionality for the following subfeature:

  * E051-09, Rename columns in the `FROM` clause (column names can be renamed in a subquery in the `FROM` clause) 

  
E061, Basic predicates and search conditions |  Oracle fully supports this feature, except that Oracle comparison of character strings differs from the standard as follows: In the standard, two character strings of unequal length are compared by either padding the shorter string with spaces or a fictitious character that is less than all actual characters. The decision on padding is made on the basis of the character set. In Oracle, the decision is based on whether the comparands are of fixed or varying length.  
E071, Basic query expressions |  Oracle fully supports the following subfeatures:

  * E071-01, `UNION` `DISTINCT` table operator 
  * E071-02, `UNION` `ALL` table operator 
  * E071-05, Columns combined by table operators need not have exactly the same type
  * E071-06, table operators in subqueries

Oracle has equivalent functionality for the following subfeature:

  * E071-03, `EXCEPT` `DISTINCT` table operator: Use `MINUS` instead of `EXCEPT` `DISTINCT`

  
E081, Basic privileges |  Oracle fully supports all subfeatures of this feature, except E081-09, `USAGE` privileges. In the standard, the `USAGE` privilege permits the user to use domains, collations, character sets, transliterations, user-defined types and sequence generators. Oracle does not support domains or transliterations. No privileges are required to access collations and character sets. The Oracle privilege to use a user-defined type is `EXECUTE`. The Oracle privilege to use a sequence type is `SELECT`.   
E091, Set functions |  Oracle fully supports this feature.  
E101, Basic data manipulation |  Oracle fully supports this feature.  
E111, Single row `SELECT` statement  |  Oracle fully supports this feature.  
E121, Basic cursor support |  Oracle fully supports the following subfeatures:

  * E121-02, `ORDER` `BY` columns need not be in `SELECT` list 
  * E121-03, Value expressions in `ORDER` `BY` clause 
  * E121-04, `OPEN` statement 
  * E121-06, Positioned `UPDATE` statement 
  * E121-07, Positioned `DELETE` statement 
  * E121-08, `CLOSE` statement 

Oracle provides partial support for the following subfeatures:

  * E121-01, `DECLARE` `CURSOR` \- fully supported, except for the `FOR` `READ` `ONLY` syntax 
  * E121-10 `FETCH` statement, implicit `NEXT` \- fully supported, except for the noise word `FROM`

Oracle provides enhanced support for the following subfeature:

  * E121-17, `WITH` `HOLD` cursors (in the standard, a cursor is not held through a `ROLLBACK`, but Oracle does hold through `ROLLBACK`) 

  
E131, Null value support |  Oracle fully supports this feature, with this exception: In Oracle, a null of character type is indistinguishable from a zero-length character string.  
E141, Basic integrity constraints |  Oracle fully supports this feature.  
E151, Transaction support |  Oracle fully supports this feature.  
E152, Basic `SET` `TRANSACTION` statement  |  Oracle fully supports this feature.  
E153, Updatable queries with subqueries |  Oracle fully supports this feature.  
E161, SQL comments using leading double minus |  Oracle fully supports this feature.  
E171, SQLSTATE support |  Oracle fully supports this feature.  
E182, Host language binding |  Oracle fully supports this feature through Pro*C/C++ and Pro*COBOL  
F021, Basic information schema |  Oracle does not have any of the views in this feature. However, Oracle makes the same information available in other metadata views:

  * Instead of `TABLES`, use `ALL_TABLES`. 
  * Instead of `COLUMNS`, use `ALL_TAB_COLUMNS`. 
  * Instead of `VIEWS`, use `ALL_VIEWS`.  However, Oracle's `ALL_VIEWS` does not display whether a user view was defined `WITH` `CHECK` `OPTION` or if it is updatable. To see whether a view has `WITH` `CHECK` `OPTION`, use `ALL_CONSTRAINTS`, with `TABLE_NAME` equal to the view name and look for `CONSTRAINT_TYPE` equal to '`V`'. 
  * Instead of `TABLE_CONSTRAINTS`, `REFERENTIAL_CONSTRAINTS`, and `CHECK_CONSTRAINTS`, use `ALL_CONSTRAINTS`.  However, Oracle's `ALL_CONSTRAINTS` does not display whether a constraint is deferrable or initially deferred. 

  
F031, Basic schema manipulation |  Oracle fully supports these subfeatures:

  * F031-01, `CREATE` `TABLE` statement to create persistent base tables 
  * F031-02, `CREATE` `VIEW` statement 
  * F031-03, `GRANT` statement 

Oracle provides equivalent support for this subfeature:

  * F031-04, `ALTER` `TABLE` statement: `ADD` `COLUMN` clause (Oracle does not support the optional keyword `COLUMN` in this syntax. Also, Oracle requires the column definition to be enclosed in parentheses, unlike the standard.) 

Oracle does not support these subfeatures (because Oracle does not support the
keyword `RESTRICT`):

  * F031-13, `DROP` `TABLE` statement: `RESTRICT` clause 
  * F031-16, `DROP` `VIEW` statement: `RESTRICT` clause 
  * F031-19, `REVOKE` statement: `RESTRICT` clause 

(Oracle `DROP` commands enhance the standard by invalidating dependent
objects, so that they can be subsequently revalidated without user action,
rather than either cascading all drops to dependent objects or prohibiting a
drop if there is a dependent object.)  
F041, Basic joined table |  Oracle fully supports this feature.  
F051, Basic date and time |  Oracle fully supports this feature, except the following subfeatures are not supported:

  * F051-02, `TIME` data type 
  * F051-07, `LOCALTIME`

  
F081, `UNION` and `EXCEPT` in views  |  Oracle fully supports `UNION` in views.   
F131, Grouped operations |  Oracle fully supports this feature.  
F181, Multiple module support |  Oracle fully supports this feature.  
F201, `CAST` function  |  Oracle fully supports this feature.  
F221, Explicit defaults |  Oracle's `DEFAULT` `ON` `NULL` capability in a column definition provides equivalent functionality for the `INSERT` statement though not for the `UPDATE` statement.   
F261, `CASE` expressions  |  Oracle fully supports this feature.  
F311, Schema definition statement |  Oracle fully supports this feature.  
F471, Scalar subquery values |  Oracle fully supports this feature.  
F481, Expanded null predicate |  Oracle fully supports this feature.  
F501, Feature and conformance views |  Oracle does not support this feature.  
F812, Basic flagging |  Oracle has a flagger, but it flags SQL-92 compliance rather than SQL:2011 compliance.  
S011, Distinct types |  Distinct types are strongly typed scalar types. A distinct type can be emulated in Oracle using an object type with only one attribute. The standard's Information Schema view called `USER_DEFINED_TYPES` is equivalent to Oracle's metadata view `ALL_TYPES`.   
T321, Basic SQL-invoked routines |  Oracle fully supports these subfeatures:

  * T321-03, function invocation
  * T321-04, `CALL` statement 

Oracle supports these subfeatures with syntactic differences:

  * T321-01, user-defined functions with no overloading
  * T321-02, user-defined procedures with no overloading

The Oracle syntax for `CREATE` `FUNCTION` and `CREATE` `PROCEDURE` differs
from the standard as follows:

  * In the standard, the mode of a parameter (`IN`, `OUT`, or `INOUT`) comes before the parameter name, whereas in Oracle it comes after the parameter name. 
  * The standard uses `INOUT`, whereas Oracle uses `IN` `OUT`. 
  * Oracle requires either `IS` or `AS` after the return type and before the definition of the routine body, while the standard lacks these keywords. 
  * If the routine body is in C (for example), then the standard uses the keywords `LANGUAGE` `C` `EXTERNAL` `NAME` to name the routine, whereas Oracle uses `LANGUAGE` `C` `NAME`. 
  * If the routine body is in SQL, then Oracle uses its proprietary procedural extension called PL/SQL.

Oracle supports the following subfeature in PL/SQL but not in Oracle SQL:

  * T321-05, `RETURN` statement 

Oracle provides equivalent functionality for the following subfeatures:

  * T321-06, `ROUTINES` view: Use the `ALL` `PROCEDURES` metadata view. 
  * T321-07, `PARAMETERS` view: Use the `ALL_ARGUMENTS` and `ALL_METHOD_PARAMS` metadata views. 

  
T631, `IN` predicate with one list element  |  Oracle fully supports this feature.


[← Previous](ISO-Standards.md)

[Next →](Oracle-Support-for-Optional-Features-of-SQLFoundation2011.md)
