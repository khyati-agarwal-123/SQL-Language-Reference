[Previous](Pseudocolumns.md) [Next](Sequence-Pseudocolumns.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Pseudocolumns](Pseudocolumns.md)
  3. Hierarchical Query Pseudocolumns 

## Hierarchical Query Pseudocolumns

The hierarchical query pseudocolumns are valid only in hierarchical queries.
The hierarchical query pseudocolumns are:

  * [CONNECT_BY_ISCYCLE Pseudocolumn](Hierarchical-Query-Pseudocolumns.md#GUID-DA181C6B-7B13-41E3-AAF5-5C19963D9D1C)

  * [CONNECT_BY_ISLEAF Pseudocolumn](Hierarchical-Query-Pseudocolumns.md#GUID-7DFBC564-31A6-4C71-A79C-6D3CC0B0BB10)

  * [LEVEL Pseudocolumn](Hierarchical-Query-Pseudocolumns.md#GUID-D91FFF59-ECB0-40F0-AB4C-7A9D27EBEEF1)

To define a hierarchical relationship in a query, you must use the `CONNECT`
`BY` clause.

### CONNECT_BY_ISCYCLE Pseudocolumn

The `CONNECT_BY_ISCYCLE` pseudocolumn returns 1 if the current row has a child
which is also its ancestor. Otherwise it returns 0.

You can specify `CONNECT_BY_ISCYCLE` only if you have specified the `NOCYCLE`
parameter of the `CONNECT` `BY` clause. `NOCYCLE` enables Oracle to return the
results of a query that would otherwise fail because of a `CONNECT` `BY` loop
in the data.

See Also:

[Hierarchical Queries](Hierarchical-
Queries.md#GUID-0118DF1D-B9A9-41EB-8556-C6E7D6A5A84E) for more information
about the `NOCYCLE` parameter and [Hierarchical Query Examples](Hierarchical-
Queries.md#GUID-E3D35EF7-33C3-4D88-81B3-00030C47AE56) for an example that
uses the `CONNECT_BY_ISCYCLE` pseudocolumn

### CONNECT_BY_ISLEAF Pseudocolumn

The `CONNECT_BY_ISLEAF` pseudocolumn returns 1 if the current row is a leaf of
the tree defined by the `CONNECT` `BY` condition. Otherwise it returns 0. This
information indicates whether a given row can be further expanded to show more
of the hierarchy.

CONNECT_BY_ISLEAF Example

The following example shows the first three levels of the `hr.employees`
table, indicating for each row whether it is a leaf row (indicated by 1 in the
`IsLeaf` column) or whether it has child rows (indicated by 0 in the `IsLeaf`
column):

    
    
    SELECT last_name "Employee", CONNECT_BY_ISLEAF "IsLeaf",
           LEVEL, SYS_CONNECT_BY_PATH(last_name, '/') "Path"
      FROM employees
      WHERE LEVEL <= 3 AND department_id = 80
      START WITH employee_id = 100
      CONNECT BY PRIOR employee_id = manager_id AND LEVEL <= 4
      ORDER BY "Employee", "IsLeaf";
    
    Employee                      IsLeaf      LEVEL Path
    ------------------------- ---------- ---------- -------------------------
    Abel                               1          3 /King/Zlotkey/Abel
    Ande                               1          3 /King/Errazuriz/Ande
    Banda                              1          3 /King/Errazuriz/Banda
    Bates                              1          3 /King/Cambrault/Bates
    Bernstein                          1          3 /King/Russell/Bernstein
    Bloom                              1          3 /King/Cambrault/Bloom
    Cambrault                          0          2 /King/Cambrault
    Cambrault                          1          3 /King/Russell/Cambrault
    Doran                              1          3 /King/Partners/Doran
    Errazuriz                          0          2 /King/Errazuriz
    Fox                                1          3 /King/Cambrault/Fox
    . . . 

See Also:

[Hierarchical Queries](Hierarchical-
Queries.md#GUID-0118DF1D-B9A9-41EB-8556-C6E7D6A5A84E) and
[SYS_CONNECT_BY_PATH](SYS_CONNECT_BY_PATH.md#GUID-D25A0F86-B559-4090-9164-7A2C84D1E11E)

### LEVEL Pseudocolumn

For each row returned by a hierarchical query, the `LEVEL` pseudocolumn
returns 1 for a root row, 2 for a child of a root, and so on. A root row is
the highest row within an inverted tree. A child row is any nonroot row. A
parent row is any row that has children. A leaf row is any row without
children. [Figure 3-1](Hierarchical-Query-
Pseudocolumns.md#GUID-D91FFF59-ECB0-40F0-AB4C-7A9D27EBEEF1__I1009270) shows
the nodes of an inverted tree with their `LEVEL` values.

Figure 3-1 Hierarchical Tree

![Description of Figure 3-1
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/sqlrf001.gif)  
[Description of "Figure 3-1 Hierarchical Tree "](img_text/sqlrf001.md)

See Also:

[Hierarchical Queries](Hierarchical-
Queries.md#GUID-0118DF1D-B9A9-41EB-8556-C6E7D6A5A84E) for information on
hierarchical queries in general and [IN Condition](IN-
Condition.md#GUID-C7961CB3-8F60-47E0-96EB-BDCF5DB1317C) for restrictions on
using the `LEVEL` pseudocolumn


[← Previous](Hierarchical-Query-Pseudocolumns.md)

[Next →](Sequence-Pseudocolumns.md)
