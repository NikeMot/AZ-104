# Lab 02 Validation

## Identity Validation

| Requirement | Status |
|---|---|
| Internal users created or reviewed | Completed |
| User properties configured or reviewed | Completed |
| Security groups created or reviewed | Completed |
| Users added to appropriate groups | Completed |
| External contractor invited or process reviewed | Completed |
| License assignment area reviewed | Completed |
| SSPR reviewed or configured | Completed |

## Resource Group Validation

| Resource group | Purpose | Status |
|---|---|---|
| `rg-az104-idgov-fin-prod-uks-001` | Production governance scope | Completed/reviewed |
| `rg-az104-idgov-fin-test-uks-001` | Test governance scope | Completed/reviewed |

## Tag Validation

Required tags:

| Tag | Purpose |
|---|---|
| `Environment` | Distinguishes production and test resources |
| `CostCenter` | Supports finance and cost reporting |
| `Owner` | Identifies responsible owner |
| `Project` | Links resources to the lab scenario |
| `Criticality` | Identifies business importance |

## Access Control Validation

- Cloud operators group granted management permissions only for the test resource group.
- Finance readers group granted read-only permissions only for the production resource group.
- External contractor did not receive Azure resource access.
- Access assignments were interpreted using IAM concepts.
- Least privilege was applied by combining role choice with scope choice.

## Governance Validation

- Production resource group protected from accidental deletion through a lock or documented equivalent.
- Policy requirement for the `CostCenter` tag reviewed or configured.
- Subscription-level access and settings reviewed.
- Management group area reviewed or configured.
- Budget alert reviewed or configured.
- Azure Advisor recommendations reviewed.

## Completion Statement

This blank lab validated the ability to translate business requirements into Azure identity, access, and governance configuration without relying on a walkthrough.
