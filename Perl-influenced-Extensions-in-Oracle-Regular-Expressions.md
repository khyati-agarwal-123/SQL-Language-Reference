[Previous](Regular-Expression-Operator-Multilingual-Enhancements.md)
[Next](Oracle-SQL-Reserved-Words-and-Keywords.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Oracle Regular Expression Support](Oracle-Regular-Expression-Support.md)
  3. Perl-influenced Extensions in Oracle Regular Expressions 

## Perl-influenced Extensions in Oracle Regular Expressions

Oracle Database regular expression functions and conditions accept a number of
Perl-influenced operators that are in common use, although not part of the
POSIX standard. [Table D-3](Perl-influenced-Extensions-in-Oracle-Regular-
Expressions.md#GUID-2D2B8DEB-1343-4DA3-BBC1-5A5C79A5FC20__CEGCDCCF "First
column lists Perl-influenced operators accepted by Oracle regular expression
functions and conditions; second column provides descriptions.") lists those
operators. For more complete descriptions with examples, refer to [Oracle
Database Development Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADFNS1012).

Table D-3 Perl-influenced Operators in Oracle Regular Expressions

Operator | Description  
---|---  
\d |  A digit character.  
\D |  A nondigit character.  
\w |  A word character.  
\W |  A nonword character.  
\s |  A whitespace character.  
\S |  A non-whitespace character.  
\A |  Matches only at the beginning of a string, or before a newline character at the end of a string.  
\Z |  Matches only at the end of a string.  
*? |  Matches the preceding pattern element 0 or more times (nongreedy).  
+? |  Matches the preceding pattern element 1 or more times (nongreedy).  
?? |  Matches the preceding pattern element 0 or 1 time (nongreedy).  
{n}? |  Matches the preceding pattern element exactly `n` times (nongreedy).   
{n,}? |  Matches the preceding pattern element at least `n` times (nongreedy).   
{n,m}? |  Matches the preceding pattern element at least `n` but not more than `m` times (nongreedy). 


[← Previous](Regular-Expression-Operator-Multilingual-Enhancements.md)

[Next →](Oracle-SQL-Reserved-Words-and-Keywords.md)
