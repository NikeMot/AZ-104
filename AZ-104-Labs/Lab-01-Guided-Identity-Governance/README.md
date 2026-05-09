# Lab 01 — Guided Identity and Governance

**Certification:** Microsoft AZ-104: Azure Administrator Associate  
**Domain:** Manage Azure identities and governance  
**Lab type:** Guided practice  
**Status:** Completed

## Scenario

This lab built the identity and governance foundation for a simulated Azure environment. The goal was to practise creating and managing Microsoft Entra identities, configuring access to Azure resources, and applying basic governance controls at subscription and resource group scope.

## AZ-104 Objectives Covered

### Manage Microsoft Entra users and groups

- Created users and groups
- Managed user and group properties
- Reviewed license assignment in Microsoft Entra ID
- Managed external users
- Configured or reviewed self-service password reset, SSPR

### Manage access to Azure resources

- Reviewed built-in Azure roles
- Assigned roles at different scopes
- Interpreted access assignments

### Manage Azure subscriptions and governance

- Created and managed resource groups
- Applied and managed tags
- Configured resource locks
- Implemented Azure Policy
- Reviewed subscriptions
- Reviewed or configured management groups
- Reviewed costs using budgets, alerts, and Azure Advisor recommendations

## Implementation Summary

The lab focused on the difference between identity management and Azure resource authorization.

Key activities included:

- reviewing the Azure tenant and subscription context
- creating dedicated lab resource groups
- applying governance tags for environment, cost centre, owner, and project
- creating Microsoft Entra users and security groups
- reviewing license assignment
- inviting an external user
- reviewing or configuring SSPR
- assigning Azure RBAC roles at resource group scope
- using IAM to interpret access assignments
- reviewing subscription-level access
- reviewing or creating a management group
- assigning a tag-related Azure Policy
- applying a resource lock
- creating or reviewing a budget alert
- reviewing Azure Advisor recommendations

## Exam Patterns Reinforced

| Requirement pattern | Correct AZ-104 thinking |
|---|---|
| Manage users, groups, and tenant identity | Microsoft Entra ID |
| Manage access to Azure resources | Azure RBAC |
| Give access to only one resource group | Assign role at resource group scope |
| Enforce required tags | Azure Policy |
| Organise and track resources | Tags |
| Prevent accidental deletion | Resource lock |
| Apply governance across subscriptions | Management group |
| Notify when spend reaches a threshold | Budget alert |
| Get cost/security/reliability recommendations | Azure Advisor |

## Key Lessons

- Microsoft Entra roles and Azure RBAC roles solve different problems.
- Azure RBAC scope matters. Permissions inherit downward from management group to subscription to resource group to resource.
- Least privilege means using the narrowest role and narrowest scope that satisfy the requirement.
- Tags are metadata; Azure Policy enforces rules.
- Resource locks can block deletion or modification even when RBAC would otherwise allow the action.
- External users still require RBAC assignments before they can access Azure resources.

## Evidence Method

No screenshots are stored in this repository. Evidence is recorded through written validation notes, access review notes, and reflection files.
