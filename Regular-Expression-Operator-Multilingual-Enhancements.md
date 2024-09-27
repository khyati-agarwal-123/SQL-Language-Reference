[Previous](Multilingual-Regular-Expression-Syntax.md) [Next](Perl-
influenced-Extensions-in-Oracle-Regular-Expressions.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Oracle Regular Expression Support](Oracle-Regular-Expression-Support.md)
  3. Regular Expression Operator Multilingual Enhancements

## Regular Expression Operator Multilingual Enhancements

When applied to multilingual data, Oracle's implementation of the POSIX
operators extends beyond the matching capabilities specified in the POSIX
standard. [Table D-2](Regular-Expression-Operator-Multilingual-
Enhancements.md#GUID-8A02D839-90A5-4FB6-AC43-7AE8CB08E8BA__G692318 "This
table is described in the preceding text.") shows the relationship of the
operators in the context of the POSIX standard.

  * The first column lists the supported operators.

  * The second and third columns indicate whether the POSIX standard (Basic Regular ExpressionâBRE and Extended Regular ExpressionâERE, respectively) defines the operator

  * The fourth column indicates whether Oracle's implementation extends the operator's semantics for handling multilingual data.

Oracle lets you enter multibyte characters directly, if you have a direct
input method, or you can use functions to compose the multibyte characters.
You cannot use the Unicode hexadecimal encoding value of the form '`\xxxx`'.
Oracle evaluates the characters based on the byte values used to encode the
character, not the graphical representation of the character. All accented
characters are considered word characters.

Table D-2 POSIX and Multilingual Operator Relationships

Operator | POSIX BRE syntax | POSIX ERE Syntax | Multilingual Enhancement  
---|---|---|---  
\ |  Yes |  Yes |  â  
* |  Yes |  Yes |  â  
+ |  \-- |  Yes |  â  
? |  â |  Yes |  â  
| |  â |  Yes |  â  
^ |  Yes |  Yes |  Yes  
$ |  Yes |  Yes |  Yes  
. |  Yes |  Yes |  Yes  
[ ] |  Yes |  Yes |  Yes  
( ) |  Yes |  Yes |  â  
{m} |  Yes |  Yes |  â  
{m,} |  Yes |  Yes |  â  
{m,n} |  Yes |  Yes |  â  
\n |  Yes |  Yes |  Yes  
[..] |  Yes |  Yes |  Yes  
[::] |  Yes |  Yes |  Yes  
[==] |  Yes |  Yes |  Yes


[← Previous](Multilingual-Regular-Expression-Syntax.md)

[Next →](Perl-influenced-Extensions-in-Oracle-Regular-Expressions.md)
