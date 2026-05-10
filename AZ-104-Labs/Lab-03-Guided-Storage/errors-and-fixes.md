# Lab 03 Errors and Fixes

| Issue | Root cause | Fix or action | AZ-104 exam lesson |
|---|---|---|---|
| Could not find containers | Containers are under the Blob service inside the storage account | Open Storage account → Data storage → Containers | A container belongs to Blob Storage; it is not the Blob service itself |
| SAS access fails | Token may be expired, missing permissions, or blocked by firewall | Check expiry, permissions, HTTPS, resource scope, and network rules | SAS requires correct permissions and reachable network path |
| User has permission but cannot access storage | Storage firewall or network restriction may be blocking access | Check storage networking, allowed IPs, VNet rules, service endpoints, or private endpoints | Identity/RBAC and network access are separate controls |
| Confusion between soft delete and versioning | Both protect data, but from different risks | Use soft delete for deleted blobs; use versioning for overwritten blobs | Match the feature to the recovery requirement |
| Lifecycle rule does not act immediately | Blob may not meet age/prefix conditions, or lifecycle processing has not run yet | Check rule scope, prefix, blob type, age condition, and wait for policy processing | Lifecycle management is rule-based and not instant |
| Object replication does not appear immediately | Versioning or replication policy may not be configured correctly | Check source/destination containers, versioning, replication rule, and supported blob type | Object replication is policy-based and different from GRS |

## Notes

The major learning point from this lab was that Azure Storage has multiple independent control layers: identity, SAS/keys, network restrictions, data protection, and lifecycle management.
