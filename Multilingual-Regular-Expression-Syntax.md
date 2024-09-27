[Previous](Oracle-Regular-Expression-Support.md) [Next](Regular-Expression-
Operator-Multilingual-Enhancements.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Oracle Regular Expression Support](Oracle-Regular-Expression-Support.md)
  3. Multilingual Regular Expression Syntax 

## Multilingual Regular Expression Syntax

[Table D-1](Multilingual-Regular-Expression-
Syntax.md#GUID-B03DEEAC-3F9E-4BFD-89D5-F481EA391D7C__BABJDBHB "Column 1
contains regular expression operators and column 2 describes Oracle Database
support of each symbol.") lists the full set of operators defined in the POSIX
standard Extended Regular Expression (ERE) syntax. Oracle follows the exact
syntax and matching semantics for these operators as defined in the POSIX
standard for matching ASCII (English language) data. For more complete
descriptions of the operators, examples of their use, and Oracle multilingual
enhancements of the operators, refer to Oracle Database Development Guide.
Notes following the table provide more complete descriptions of the operators
and their functions, as well as Oracle multilingual enhancements of the
operators. [Table D-2](Regular-Expression-Operator-Multilingual-
Enhancements.md#GUID-8A02D839-90A5-4FB6-AC43-7AE8CB08E8BA__G692318 "This
table is described in the preceding text.") summarizes Oracle support for and
multilingual enhancement of the POSIX operators.

Table D-1 Regular Expression Operators and Metasymbols

Operator | Description  
---|---  
\  |  The backslash character can have four different meanings depending on the context. It can:

  * Stand for itself
  * Quote the next character
  * Introduce an operator
  * Do nothing

  
* |  Matches zero or more occurrences  
+ |  Matches one or more occurrences  
? |  Matches zero or one occurrence  
| |  Alternation operator for specifying alternative matches  
^  |  Matches the beginning of a string by default. In multiline mode, it matches the beginning of any line anywhere within the source string.  
$  |  Matches the end of a string by default. In multiline mode, it matches the end of any line anywhere within the source string.  
.  |  Matches any character in the supported character set except `NULL`  
[ ]  |  Bracket expression for specifying a matching list that should match any one of the expressions represented in the list. A non-matching list expression begins with a circumflex (^) and specifies a list that matches any character except for the expressions represented in the list. To specify a right bracket (]) in the bracket expression, place it first in the list (after the initial circumflex (^), if any). To specify a hyphen in the bracket expression, place it first in the list (after the initial circumflex (^), if any), last in the list, or as an ending range point in a range expression.  
( ) |  Grouping expression, treated as a single subexpression  
{m}  |  Matches exactly m times  
{m,} |  Matches at least m times  
{m,n} |  Matches at least m times but no more than n times  
\n  |  The backreference expression (n is a digit between 1 and 9) matches the nth subexpression enclosed between '(' and ')' preceding the \n   
[..]  |  Specifies one collation element, and can be a multicharacter element (for example, [.ch.] in Spanish)  
[: :]  |  Specifies character classes (for example, [:alpha:]). It matches any character within the character class.  
[==]  |  Specifies equivalence classes. For example, [=a=] matches all characters having base letter 'a'.


[← Previous](Oracle-Regular-Expression-Support.md)

[Next →](Regular-Expression-Operator-Multilingual-Enhancements.md)
