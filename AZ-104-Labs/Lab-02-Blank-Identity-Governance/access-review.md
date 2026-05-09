# Lab 02 Access Review

## Access Model

This lab used group-based access where possible. The goal was to avoid direct user assignments and apply least privilege at the narrowest valid scope.

| Principal | Type | Role | Scope | Access source | Least privilege reasoning |
|---|---|---|---|---|---|
| Daniel Reed | User | N/A directly | N/A | Group-based | User access should come through the cloud operators group |
| `grp-az104-finance-cloud-operators` | Security group | Contributor or suitable management role | Test resource group only | Direct group assignment | Allows management of non-production resources without subscription-wide access |
| Maya Singh | User | N/A directly | N/A | Group-based | User access should come through the finance readers group |
| `grp-az104-finance-readers` | Security group | Reader | Production resource group only | Direct group assignment | Allows visibility without modification rights |
| External contractor | Guest user | None | None | No Azure RBAC assignment | Identity exists but resource access is not required yet |

## Direct vs Group-Based Access

The preferred model is:

```text
User -> Security group -> Azure RBAC role assignment -> Scope
```

This is better than direct user assignment because group membership can be changed without modifying the RBAC assignment itself.

## Scope Review

Azure RBAC scope hierarchy:

```text
Management group
└── Subscription
    └── Resource group
        └── Resource
```

The lab reinforced that assigning a role at a parent scope causes inheritance to child scopes.

## Exam Lessons

- Assigning Contributor at subscription scope is too broad when the requirement only mentions one resource group.
- Reader is appropriate for view-only access.
- Owner should not be used unless the user must manage both resources and access.
- User Access Administrator is for managing role assignments, not normal resource management.
- A guest user still requires Azure RBAC before they can access Azure resources.
