# Lab 01 Validation

## Tenant and Subscription Review

- Azure tenant reviewed.
- Active subscription reviewed.
- Subscription context confirmed before creating resources.
- Role and permission boundaries considered.

## Resource Groups

| Resource group | Purpose | Validation |
|---|---|---|
| `rg-az104-idgov-prod-uks-001` | Production governance scope | Created/reviewed |
| `rg-az104-idgov-test-uks-001` | Test governance scope | Created/reviewed |

## Tags

Required tags were applied or reviewed:

| Tag | Purpose |
|---|---|
| `Environment` | Identifies production or test resources |
| `CostCenter` | Supports cost tracking |
| `Owner` | Identifies responsible person/team |
| `Project` | Links resources to the lab/project |

## Identity Validation

- Internal users created or reviewed.
- User properties updated or reviewed.
- Security groups created or reviewed.
- Users added to appropriate groups.
- License assignment area reviewed.
- External user invitation process reviewed.
- SSPR reviewed or configured for a selected group.

## Access Control Validation

- Built-in Azure roles reviewed.
- Role assignments applied at resource group scope.
- Access assignments checked through IAM.
- Direct, group-based, and inherited access concepts reviewed.

## Governance Validation

- Subscription settings reviewed.
- Management group area reviewed.
- Azure Policy assignment reviewed or configured.
- Resource lock applied or reviewed.
- Budget alert reviewed or configured.
- Azure Advisor recommendations reviewed.

## Completion Statement

This lab validated the core identity and governance tasks required for the AZ-104 Manage Azure identities and governance domain.
