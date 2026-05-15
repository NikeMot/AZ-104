# AZ-104 Azure Administrator Labs

This repository documents hands-on preparation for the **Microsoft AZ-104: Azure Administrator Associate** exam.

The lab programme converts AZ-104 course knowledge into practical Azure administration skill. Each completed lab documents the scenario, objectives covered, implementation summary, validation evidence, exam patterns, and lessons learned.

## Current Progress

| Lab | Status | Domain | Type |
|---|---|---|---|
| Lab 01 | Completed | Manage Azure identities and governance | Guided practice |
| Lab 02 | Completed | Manage Azure identities and governance | Blank from-scratch challenge |
| Lab 03 | Completed | Implement and manage storage | Guided practice |
| Lab 04 | Completed | Implement and manage storage | Blank from-scratch challenge |
| Lab 05 | Completed | Implement and manage virtual networking | Guided networking architecture lab |
| Lab 06 | Completed | Implement and manage virtual networking | Blank from-scratch challenge |

Only completed labs are uploaded to this repository.

## AZ-104 Exam Readiness Method

The lab method focuses on the way AZ-104 questions are usually framed:

- identify the correct Azure service, feature, or control plane
- apply least privilege
- choose the narrowest valid RBAC scope
- distinguish Microsoft Entra roles from Azure RBAC roles
- distinguish tags from Azure Policy
- distinguish resource locks from RBAC permissions
- validate access assignments and inheritance
- distinguish storage access controls from storage data protection features
- distinguish service endpoints from private endpoints
- distinguish NSGs from UDRs
- distinguish Bastion admin access from public application frontend access
- use Network Watcher tools based on the troubleshooting layer being tested

## Repository Structure

```text
AZ-104-Labs/
├── Lab-01-Guided-Identity-Governance/
├── Lab-02-Blank-Identity-Governance/
├── Lab-03-Guided-Storage/
├── Lab-04-Blank-Storage/
├── Lab-05-Guided-Networking/
│   ├── README.md
│   ├── dns.md
│   ├── questions.md
│   ├── validation.md
│   ├── troubleshooting.md
│   └── reflection.md
└── Lab-06-Blank-Networking/
    ├── README.md
    ├── validation.md
    ├── troubleshooting.md
    └── reflection.md
```

## Completed Domains

### Manage Azure identities and governance

The completed labs cover:

- Microsoft Entra users and groups
- user and group properties
- license management review
- external users
- self-service password reset, SSPR
- built-in Azure roles
- RBAC role assignment at different scopes
- access assignment interpretation
- resource groups
- tags
- resource locks
- Azure Policy
- subscriptions
- management groups
- budgets and cost alerts
- Azure Advisor recommendations

### Implement and manage storage

The completed labs cover:

- storage accounts
- Azure Storage redundancy
- storage firewalls and virtual networks
- shared access signatures, SAS
- stored access policies
- access keys and key rotation
- identity-based access for Azure Files
- blob containers
- Azure file shares
- storage tiers
- blob lifecycle management
- blob versioning
- soft delete
- Azure Files snapshots
- Storage Explorer and AzCopy concepts

### Implement and manage virtual networking

The completed networking labs cover:

- virtual networks and subnets
- VNet peering
- public IP addresses
- user-defined routes
- NSGs and ASGs
- effective security rules
- Azure Bastion
- service endpoints
- private endpoints
- Azure DNS and private DNS for private endpoint resolution
- public Azure Load Balancer
- health probes, backend pools, and load balancing rules
- Network Watcher troubleshooting tools including IP flow verify, Next hop, effective routes, effective security rules, and Connection Monitor
- from-scratch architecture design from business requirements

## Notes

This repository intentionally avoids uploading screenshots or secrets. Evidence is documented through written validation notes, command summaries, access reviews, troubleshooting notes, and reflection files.
