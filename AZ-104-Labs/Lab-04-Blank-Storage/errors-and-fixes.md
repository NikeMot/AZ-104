# Lab 04 Errors and Fixes

| Issue | Root cause | Fix or action | AZ-104 exam lesson |
|---|---|---|---|
| Risk of using access keys for temporary access | Access keys are easy to use but too broad | Use SAS for temporary limited access | Use least privilege for storage access |
| SAS may fail | Expiry, permissions, protocol, resource scope, or firewall can be wrong | Check SAS permissions, expiry, HTTPS, and network rules | SAS requires both valid token settings and reachable network path |
| User has permission but cannot access storage | Storage firewall or network restrictions may block access | Check storage account networking and allowed subnet/IP settings | Permission and network path are separate |
| Confusion between data protection features | Soft delete, versioning, snapshots, and lifecycle policies solve different problems | Match the feature to the recovery or cost requirement | Read the exact exam wording carefully |
| Object replication unavailable or delayed | Versioning, policy, account support, or region requirements may not be met | Check prerequisites and document limitations | Object replication is policy-based and different from redundancy |

## Notes

The lab was completed confidently and the AZ-104-style questions were answered correctly. No critical storage access or data protection misunderstanding remains.
