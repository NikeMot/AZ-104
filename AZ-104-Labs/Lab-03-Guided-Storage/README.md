# Lab 03 — Guided Storage

**Certification:** Microsoft AZ-104: Azure Administrator Associate  
**Domain:** Implement and manage storage  
**Lab type:** Guided practice  
**Status:** Completed

## Scenario

This lab implemented Azure Storage for a simulated retail analytics environment. The storage design supported application logs, finance exports, shared operational files, archived reports, secure temporary access, data protection, lifecycle management, replication, encryption, and data movement.

## AZ-104 Objectives Covered

### Configure access to storage

- Configured Azure Storage firewalls and virtual network access
- Created and used shared access signature, SAS, tokens
- Configured stored access policies
- Reviewed and managed access keys
- Reviewed identity-based access for Azure Files

### Configure and manage storage accounts

- Created and configured storage accounts
- Reviewed and configured Azure Storage redundancy
- Reviewed or configured object replication
- Reviewed storage account encryption
- Managed data by using Azure Storage Explorer and AzCopy

### Configure Azure Files and Azure Blob Storage

- Created and configured Azure Files file shares
- Created and configured Azure Blob containers
- Configured storage tiers
- Configured soft delete for blobs and containers
- Configured snapshots and soft delete for Azure Files
- Configured blob lifecycle management
- Configured blob versioning

## Implementation Summary

Key activities included:

- creating a dedicated storage resource group
- creating a general-purpose v2 storage account
- reviewing secure transfer, TLS, redundancy, and encryption settings
- reviewing storage account access keys and documenting why they are sensitive
- creating blob containers for logs and reports
- uploading blobs and changing access tiers
- creating and testing SAS access
- configuring or reviewing stored access policies
- creating a VNet/subnet and restricting storage account network access
- creating an Azure Files share
- enabling file share soft delete and creating a snapshot
- enabling blob and container soft delete
- enabling blob versioning
- creating a lifecycle management rule
- creating or reviewing object replication requirements
- reviewing identity-based access options for Azure Files
- using Storage Explorer and AzCopy concepts for data management

## Exam Patterns Reinforced

| Requirement pattern | Correct AZ-104 thinking |
|---|---|
| Temporary limited access to blobs | Use SAS |
| Centrally revoke SAS access | Use a stored access policy |
| Full account-level storage secret | Access key, but avoid sharing where possible |
| Restrict storage to selected networks | Storage firewall and VNet rules/service endpoint |
| Recover deleted blobs or containers | Soft delete |
| Recover overwritten blob data | Blob versioning |
| Recover previous state of Azure Files | File share snapshot |
| Move older blobs to Cool or Archive | Lifecycle management |
| Replicate selected blobs between accounts | Object replication |
| Bulk copy data to/from storage | AzCopy |
| GUI-based storage management | Azure Storage Explorer |
| User/group access to Azure Files | Identity-based access for Azure Files |

## Key Lessons

- Azure Storage access is layered: identity permissions, SAS/keys, and network rules are separate controls.
- A user can have permission but still be blocked by the storage firewall.
- Access keys are broad account-level secrets and should not be used for temporary delegated access.
- SAS tokens should be scoped, time-limited, and restricted to HTTPS where possible.
- Stored access policies improve SAS manageability and revocation.
- Blob soft delete, container soft delete, blob versioning, Azure Files snapshots, and lifecycle management solve different problems.
- Object replication is different from storage account geo-redundancy.

## Evidence Method

No screenshots are stored in this repository. Evidence is recorded through written validation notes, access review notes, and reflection files.
