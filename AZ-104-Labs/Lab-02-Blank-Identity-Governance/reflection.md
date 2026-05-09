# Lab 02 Reflection

## What this lab tested

This lab tested whether Identity and Governance tasks could be completed from requirements rather than from guided instructions.

The main skill was translating business language into Azure configuration decisions.

## Most important decisions

1. Use Microsoft Entra ID for users, groups, external users, and SSPR.
2. Use Azure RBAC for access to Azure resources.
3. Assign access to groups rather than individual users where possible.
4. Assign roles at the narrowest valid scope.
5. Use Reader for view-only access.
6. Use Contributor or a more specific role for resource management.
7. Avoid Owner unless access management is required.
8. Use Azure Policy to enforce required tags.
9. Use resource locks to prevent accidental deletion.
10. Use budgets and Azure Advisor for cost visibility and recommendations.

## Exam patterns reinforced

- Least privilege requires both the correct role and the correct scope.
- External user invitation does not equal Azure resource access.
- Direct, group-based, and inherited access must be interpreted carefully.
- Tags are useful for organisation and cost tracking, but policy is required for enforcement.
- Locks are separate from RBAC and can block actions even for privileged users.

## What to keep reviewing

- Entra role vs Azure RBAC role decisions
- RBAC scope inheritance
- Built-in role selection
- Policy vs tag use cases
- Delete lock vs read-only lock
- Management group vs subscription vs resource group scope

## Readiness judgement

This lab provides evidence of practical readiness for the Identity and Governance section of AZ-104, provided the access model and governance controls can be explained without notes.
