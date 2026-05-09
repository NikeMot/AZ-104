# Lab 01 Errors and Fixes

| Issue | Root cause | Fix or action | AZ-104 exam lesson |
|---|---|---|---|
| Permission limitations may affect Entra, SSPR, RBAC, Policy, or management group tasks | Some tasks require elevated roles such as Global Administrator, User Administrator, Owner, User Access Administrator, or Resource Policy Contributor | Document the limitation and identify the required permission | Azure administration is role-bound; not every admin can perform every task |
| User cannot see expected resources | User may not be in the correct group, role may be assigned at wrong scope, or RBAC propagation may not have completed | Check IAM, group membership, assigned role, scope, and tenant context | Access assignment interpretation is a key AZ-104 skill |
| Resource group cannot be deleted | A delete lock may be applied | Remove the lock before deletion | Resource locks can override normal delete permissions |
| Tag requirement is not enforced | Tags alone do not enforce compliance | Use Azure Policy to require or audit tags | Tags classify; Policy enforces |

## Notes

No unresolved blockers were recorded for the completed documentation version of this lab.
