##  DROP AUDIT POLICY (Unified Auditing) {#GUID-811D3F84-744E-47A1-B69D-C9D2FA4A0844} 

This section describes the ` DROP ` ` AUDIT ` ` POLICY ` statement for  unified  auditing  . This type of auditing is new beginning with Oracle Database 12 *c* and provides a full set of enhanced auditing features. Refer to [ *Oracle Database Security Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DBSEG630) for more information on unified auditing. 

Purpose 

Use the ` DROP ` ` AUDIT ` ` POLICY ` statement to remove a unified audit policy from the database. 

> **note:** See Also: 

  * [ CREATE AUDIT POLICY (Unified Auditing) ](CREATE-AUDIT-POLICY-Unified-Auditing.md#GUID-8D6961FB-2E50-46F5-81F7-9AEA314FC693)

  * [ ALTER AUDIT POLICY (Unified Auditing) ](ALTER-AUDIT-POLICY-Unified-Auditing.md#GUID-CC41B5C2-09F4-40BC-B7FD-3B4C0A3F5437)

  * [ AUDIT (Unified Auditing) ](AUDIT-Unified-Auditing.md#GUID-B24D6874-4053-4E66-8238-6CD0C87E9DCA)

  * [ NOAUDIT (Unified Auditing) ](NOAUDIT-Unified-Auditing.md#GUID-EB92BE04-B09C-493F-952E-9629E739900E)




Prerequisites 

You must have the ` AUDIT ` ` SYSTEM ` system privilege or the ` AUDIT_ADMIN ` role. 

To drop a common unified audit policy, the current container must be the root and you must have the commonly granted ` AUDIT ` ` SYSTEM ` privilege or the ` AUDIT_ADMIN ` common role. To drop a local unified audit policy, the current container must be the container in which the audit policy was created and you must have the commonly granted ` AUDIT ` ` SYSTEM ` privilege or the ` AUDIT_ADMIN ` common role, or you must have the locally granted ` AUDIT ` ` SYSTEM ` privilege or the ` AUDIT_ADMIN ` local role in the container. 

Syntax 

*drop_audit_policy* ::= 

![Description of drop_audit_policy.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_audit_policy.gif)[ Description of the illustration drop_audit_policy.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/drop_audit_policy.md)

Semantics 

*policy* 

Specify the name of the unified audit policy you want to drop. The policy must have been created using the ` CREATE ` ` AUDIT ` ` POLICY ` statement. 

You can find the names of all unified audit policies by querying the ` AUDIT_UNIFIED_POLICIES ` view and the names of all *enabled* unified audit policies by querying the ` AUDIT_UNIFIED_ENABLED_POLICIES ` view 

Restriction on Dropping Unified Audit Policies 

You cannot drop an enabled unified audit policy. You must first disable the policy using the ` NOAUDIT ` statement. 

> **note:** See Also: 

  * [ CREATE AUDIT POLICY (Unified Auditing) ](CREATE-AUDIT-POLICY-Unified-Auditing.md#GUID-8D6961FB-2E50-46F5-81F7-9AEA314FC693)

  * *Oracle Database Reference* for more information on the [ ` AUDIT_UNIFIED_POLICIES ` ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN29157) and [ ` AUDIT_UNIFIED_ENABLED_POLICIES ` ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN29158) views 




Examples 

Dropping a Unified Audit Policy: Example 

The following statement drops unified audit policy ` table_pol ` : 
    
    
    ```
    DROP AUDIT POLICY table_pol;
    ```
