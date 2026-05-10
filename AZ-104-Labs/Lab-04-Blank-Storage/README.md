# Lab 04 — Blank Storage Challenge

**Certification:** Microsoft AZ-104: Azure Administrator Associate  
**Domain:** Implement and manage storage  
**Lab type:** Blank from-scratch challenge  
**Status:** Completed

## Scenario

This lab tested the ability to implement and manage Azure Storage from business requirements without step-by-step guidance. The simulated company needed secure storage for application logs, case reports, finance files, controlled contractor access, network restrictions, data protection, lifecycle-based cost optimisation, and replication review.

## AZ-104 Objectives Covered

### Configure access to storage

- Configured or reviewed Azure Storage firewalls and virtual networks
- Created or reviewed shared access signature, SAS, tokens
- Configured or reviewed stored access policies
- Reviewed access keys and their security implications
- Reviewed identity-based access for Azure Files

### Configure and manage storage accounts

- Created and configured storage accounts
- Reviewed Azure Storage redundancy
- Configured or reviewed object replication
- Reviewed storage account encryption
- Used or reviewed Azure Storage Explorer and AzCopy

### Configure Azure Files and Azure Blob Storage

- Created Azure Blob containers
- Created Azure Files file shares
- Configured storage tiers
- Configured or reviewed soft delete for blobs and containers
- Configured or reviewed snapshots and soft delete for Azure Files
- Configured or reviewed blob lifecycle management
- Configured or reviewed blob versioning

## Implementation Summary

The blank challenge required translating storage requirements into Azure Storage configuration decisions.

Key areas included:

- storage account creation and baseline security settings
- private blob containers for logs and reports
- blob upload and access tier configuration
- SAS-based temporary access
- stored access policy review for SAS governance
- access key review without exposing secrets
- storage firewall and VNet/subnet access controls
- Azure Files share creation and protection features
- identity-based Azure Files access review
- blob soft delete, container soft delete, versioning, and lifecycle management
- object replication review
- data movement with Storage Explorer and AzCopy

## Exam Patterns Reinforced

| Requirement pattern | Correct AZ-104 thinking |
|---|---|
| Temporary limited access | SAS token |
| Centrally manage SAS access | Stored access policy |
| Full account-level secret | Access key |
| Restrict access by network | Storage firewall and VNet rules |
| Recover deleted blobs | Blob soft delete |
| Recover deleted containers | Container soft delete |
| Recover overwritten blobs | Blob versioning |
| Recover a file share state | Azure Files snapshot |
| Move old blobs to Cool/Archive | Lifecycle management |
| Replicate selected blobs | Object replication |
| GUI-based data management | Azure Storage Explorer |
| Command-line bulk copy | AzCopy |

## Key Lessons

- Storage account security is layered across identity, network, and secret-based access controls.
- SAS should be used instead of account keys for temporary delegated access.
- Stored access policies provide better manageability for SAS access.
- Storage firewall rules can block access even when RBAC permissions are correct.
- Soft delete, versioning, snapshots, lifecycle management, and object replication each solve different problems.
- No access keys, SAS tokens, or connection strings should be committed to GitHub.

## Readiness Statement

This lab was completed confidently, and the associated AZ-104-style questions were answered correctly. The storage domain is ready to progress into virtual networking.
