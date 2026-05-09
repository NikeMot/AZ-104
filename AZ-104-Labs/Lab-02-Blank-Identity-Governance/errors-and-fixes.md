# Lab 02 Errors and Fixes

| Issue | Root cause | Fix or action | AZ-104 exam lesson |
|---|---|---|---|
| Risk of assigning access too broadly | Blank lab requirements can tempt subscription-level assignment | Use resource group scope when only one resource group is required | Scope is one of the most important AZ-104 patterns |
| External contractor cannot access resources | Guest invitation only creates an identity | Assign Azure RBAC only when access is required | Identity and authorization are separate |
| Tag requirement not enforced by manual tags | Tags are metadata, not enforcement | Use Azure Policy for required tags | Tags classify; Policy enforces |
| User cannot perform role assignments with Contributor | Contributor does not manage access | Use Owner or User Access Administrator where appropriate | Contributor can manage resources but not grant access |
| Resource cannot be deleted | Delete lock blocks deletion | Remove the lock if deletion is intentional | Locks can override normal delete capability |

## Notes

The key risk in this lab was over-permissioning. The correct exam mindset is to choose the minimum role and minimum scope that satisfy the requirement.
