# Lab 03 Reflection

## What this lab reinforced

This lab reinforced how Azure Storage is configured, secured, protected, and managed over time.

The most important concept was that storage access is layered:

- management-plane access through Azure RBAC
- data-plane access through RBAC, SAS, access keys, or identity-based access
- network access through firewalls, VNet rules, service endpoints, or private endpoints
- data protection through soft delete, versioning, snapshots, and replication
- data lifecycle through access tiers and lifecycle management

## AZ-104 patterns learned

1. Use SAS for temporary limited access.
2. Use stored access policies when SAS access must be managed centrally.
3. Avoid sharing storage account keys unless broad account-level access is genuinely required.
4. Use storage firewalls and VNet rules for network restriction.
5. Use blob soft delete to recover deleted blobs.
6. Use container soft delete to recover deleted containers.
7. Use blob versioning to recover previous versions after overwrite.
8. Use Azure Files snapshots to recover previous file share states.
9. Use lifecycle management to move or delete blobs automatically based on rules.
10. Use object replication to replicate selected blobs between storage accounts.
11. Use AzCopy for efficient command-line data movement.
12. Use Storage Explorer for GUI-based storage management.

## Exam readiness notes

Storage questions often test which feature best matches the requirement. The wording matters:

- temporary access means SAS
- central SAS revocation means stored access policy
- deleted blob recovery means soft delete
- overwritten blob recovery means versioning
- file share point-in-time recovery means snapshot
- old data tiering means lifecycle management
- selected blob replication means object replication
- private/network-restricted access means firewall, VNet rules, service endpoint, or private endpoint

## Review items

- Continue drilling SAS vs access keys.
- Continue drilling stored access policies.
- Continue drilling storage firewall vs RBAC.
- Continue drilling soft delete vs versioning vs snapshots.
- Continue drilling redundancy vs object replication.
