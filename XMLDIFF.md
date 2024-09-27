[Previous](XMLCONCAT.md) [Next](XMLELEMENT.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. XMLDIFF 

## XMLDIFF

Syntax

![Description of xmldiff.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/xmldiff.gif)  
[Description of the illustration xmldiff.eps](img_text/xmldiff.md)

Purpose

The `XMLDiff` function is the SQL interface for the XmlDiff C API. This
function compares two XML documents and captures the differences in XML
conforming to an Xdiff schema. The diff document is returned as an XMLType
document.

  * For the first two arguments, specify the names of two XMLType documents.

  * For the `integer`, specify a number representing the hashLevel for a C function XmlDiff. If you do not want hashing, set this argument to 0 or omit it entirely. If you do not want hashing, but you want to specify flags, then you must set this argument to 0. 

  * For `string`, specify the flags that control the behavior of the function. These flags are specified by one or more names separated by semicolon. The names are the same as the names of constants for XmlDiff function. 

See Also:

[Oracle XML Developer's Kit Programmer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADXDK2510) for more information on using this function,
including examples, and [Oracle Database XML C API
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=CAXML6192) for information on the XML APIs for C

Examples

The following example compares two XML documents and returns the difference as
an XMLType document:

    
    
    SELECT XMLDIFF(
    XMLTYPE('<?xml version="1.0"?>
    <bk:book xmlns:bk="http://example.com">
       <bk:tr>
            <bk:td>
                    <bk:chapter>
                            Chapter 1.
                    </bk:chapter>
            </bk:td>
            <bk:td>
                     <bk:chapter>
                            Chapter 2.
                    </bk:chapter>
            </bk:td>
       </bk:tr>
    </bk:book>'),
    XMLTYPE('<?xml version="1.0"?>
    <bk:book xmlns:bk="http://example.com">
       <bk:tr>
            <bk:td>
                    <bk:chapter>
                            Chapter 1.
                    </bk:chapter>
            </bk:td>
            <bk:td/>
       </bk:tr>
    </bk:book>')
    )
    FROM DUAL; 


[← Previous](XMLCONCAT.md)

[Next →](XMLELEMENT.md)
