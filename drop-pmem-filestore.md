[Previous](DROP-PLUGGABLE-DATABASE.md) [Next](DROP-PROCEDURE.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP PMEM FILESTORE

## DROP PMEM FILESTORE

Purpose

You can drop a PMEM file store with this command.

Syntax

drop_pmem_filestore::=

  

![Description of drop_pmem_fs.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_pmem_fs.gif)  
[Description of the illustration drop_pmem_fs.eps](img_text/drop_pmem_fs.md)

  

Semantics

INCLUDING CONTENTS

Specify `INCLUDING CONTENTS` to confirm that Oracle should remove all the
files in the PMEM file store.

EXCLUDING CONTENTS

Specify `EXCLUDING CONTENTS` to ensure that Oracle drops the PMEM file store
only when the file store is empty.

FORCE

Specify `FORCE` along with `INCLUDING CONTENTS` if you suspect that the file
store is corrupt.

Note that this option does not check if the file store has content in it prior
to deleting it.

If you specify neither `INCLUDING CONTENTS` nor `EXCLUDING CONTENTS`, you must
ensure that the file store is empty. `EXCLUDING CONTENTS` is the default
behavior.

Example

    
    
    DROP PMEM FILESTORE cloud_db_1 EXCLUDING CONTENTS


[← Previous](DROP-PLUGGABLE-DATABASE.md)

[Next →](DROP-PROCEDURE.md)
