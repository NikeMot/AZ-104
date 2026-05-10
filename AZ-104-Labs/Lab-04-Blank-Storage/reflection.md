# Lab 04 Reflection

## What this lab tested

This lab tested the ability to complete Azure Storage requirements without guided instructions.

The main skill was matching business requirements to the correct Azure Storage feature.

## Most important decisions

1. Use SAS for temporary limited access.
2. Use stored access policies for central SAS management.
3. Avoid exposing access keys.
4. Use storage firewall and VNet rules for network restrictions.
5. Use blob soft delete for deleted blob recovery.
6. Use container soft delete for deleted container recovery.
7. Use blob versioning for overwrite protection.
8. Use Azure Files snapshots for file share point-in-time recovery.
9. Use lifecycle management for automatic tiering or deletion.
10. Use object replication for selected blob replication between accounts.
11. Use Storage Explorer for GUI-based storage management.
12. Use AzCopy for command-line data transfer.

## Exam patterns reinforced

- Storage security is layered across permissions, network path, and secrets.
- The exam often tests the difference between similar data protection features.
- SAS and access keys are not interchangeable from a least-privilege perspective.
- Object replication and storage redundancy are different concepts.
- Identity-based access for Azure Files is used when user/group-based file access is required.

## Readiness judgement

The storage domain was completed confidently and the AZ-104-style questions were answered correctly. This indicates readiness to progress to the virtual networking domain.

## Review items

- Continue reviewing storage firewall vs RBAC.
- Continue reviewing SAS vs access keys.
- Continue reviewing soft delete vs versioning vs snapshots.
- Continue reviewing object replication vs GRS/RA-GRS.
