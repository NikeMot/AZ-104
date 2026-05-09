# Lab 02 — Blank Identity and Governance Challenge

**Certification:** Microsoft AZ-104: Azure Administrator Associate  
**Domain:** Manage Azure identities and governance  
**Lab type:** Blank from-scratch challenge  
**Status:** Completed

## Scenario

This lab repeated the Identity and Governance domain without step-by-step guidance. The objective was to apply the same AZ-104 identity, access, and governance skills from a business requirement rather than a walkthrough.

The simulated company required a governed Azure structure for a finance operations platform, with least-privilege access, auditable permissions, resource protection, and cost visibility.

## AZ-104 Objectives Covered

### Manage Microsoft Entra users and groups

- Created or reviewed internal users
- Managed user properties
- Created security groups
- Added users to groups
- Reviewed license assignment
- Invited an external user
- Reviewed or configured SSPR

### Manage access to Azure resources

- Selected appropriate built-in Azure roles
- Assigned roles at the correct scope
- Interpreted direct, group-based, and inherited access
- Applied least privilege

### Manage Azure subscriptions and governance

- Created or reviewed resource groups
- Applied tags
- Configured or reviewed Azure Policy
- Configured or reviewed resource locks
- Reviewed subscription settings
- Reviewed or configured management groups
- Reviewed or configured budget alerts
- Reviewed Azure Advisor recommendations

## Implementation Summary

The lab required translating business requirements into Azure configuration decisions.

Key tasks included:

- creating finance-focused users and groups
- using group-based access rather than direct user assignments
- assigning Contributor access only to a test resource group
- assigning Reader access only to a production resource group
- ensuring an external contractor had no Azure resource access until required
- applying tags for ownership, project, cost centre, environment, and criticality
- applying governance controls through Azure Policy and resource locks
- reviewing subscription, management group, budget, and Advisor areas

## Exam Patterns Reinforced

| Exam wording | Correct interpretation |
|---|---|
| `Manage resources only in this resource group` | Assign an Azure RBAC role at resource group scope |
| `View but not modify production resources` | Assign Reader at the production resource group scope |
| `External contractor needs identity but no resource access yet` | Invite guest user but do not assign RBAC |
| `Require CostCenter tag` | Use Azure Policy |
| `Prevent accidental deletion` | Use a Delete lock |
| `Notify when spend reaches 80%` | Use a budget alert |
| `Apply governance across subscriptions` | Use a management group |

## Key Lessons

- Blank labs reveal whether the concept is actually understood.
- Least privilege is usually a combination of the correct role and the correct scope.
- Group-based RBAC assignments are easier to manage and audit than direct user assignments.
- External identity and Azure resource access are separate steps.
- Azure Policy is for governance enforcement; tags alone are not enough.
- Locks protect resources from accidental deletion or modification.

## Completion Standard

This lab is considered complete when the identity model, RBAC assignments, governance controls, access review, and reflection have been documented.
