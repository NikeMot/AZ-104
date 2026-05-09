# Lab 01 Reflection

## What this lab reinforced

This lab reinforced the foundation of Azure administration: identity, access, scope, governance, and cost control.

The most important pattern was the separation between:

- Microsoft Entra ID for identity and tenant administration
- Azure RBAC for Azure resource access
- Azure Policy for governance enforcement
- resource locks for delete/modify protection
- budgets and Advisor for cost visibility and recommendations

## AZ-104 patterns learned

1. Use Microsoft Entra roles for identity administration.
2. Use Azure RBAC for Azure resource permissions.
3. Assign access to groups where possible.
4. Use the narrowest role and scope that satisfy the requirement.
5. Tags organise resources but do not enforce rules.
6. Azure Policy enforces or audits governance rules.
7. Resource locks can prevent deletion even when a user has broad RBAC permissions.
8. Management groups are used for governance across subscriptions.
9. Budget alerts are used for cost threshold notifications.
10. Azure Advisor provides recommendations, not enforcement.

## Exam readiness notes

This domain is heavily focused on decision-making:

- Which control plane is being used?
- What scope should be selected?
- What is the least privileged role?
- Is the requirement asking for classification, enforcement, or protection?

## Review items

- Continue drilling Entra roles vs Azure RBAC roles.
- Continue drilling scope inheritance.
- Continue drilling tags vs Azure Policy.
- Continue drilling locks vs RBAC permissions.
