##  DROP FLASHBACK ARCHIVE {#GUID-FFF61E62-28AF-4F7B-BBD7-8D9AC08DDE77} 

Purpose 

Use the ` DROP ` ` FLASHBACK ` ` ARCHIVE ` clause to remove a flashback archive from the system. This statement removes the flashback archive and all the historical data in it, but does not drop the tablespaces that were used by the flashback archive. 

Prerequisites 

You must have the ` FLASHBACK ` ` ARCHIVE ` ` ADMINISTER ` system privilege to drop a flashback archive. 

Syntax 

*drop_flashback_archive* ::= 

![Description of drop_flashback_archive.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_flashback_archive.gif)[ Description of the illustration drop_flashback_archive.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/drop_flashback_archive.md)

Semantics 

*flashback_archive* 

Specify the name of the flashback archive you want to drop. 

> **note:** See Also: 

[ CREATE FLASHBACK ARCHIVE ](CREATE-FLASHBACK-ARCHIVE.md#GUID-9E821EC5-8350-4729-85FE-2188EBB4139B) for information on creating flashback archives and for some simple examples of using flashback archives 
