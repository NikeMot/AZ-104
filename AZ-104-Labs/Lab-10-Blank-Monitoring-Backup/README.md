# Lab 10 — Blank Monitoring, Backup, and Recovery Challenge

**Certification:** Microsoft AZ-104: Azure Administrator Associate  
**Domain:** Monitor and maintain Azure resources  
**Lab type:** Blank from-scratch challenge  
**Status:** Completed  
**Difficulty:** Harder than exam

## Scenario Summary

This lab required designing the monitoring, alerting, backup, restore, and disaster recovery layer for a production SaaS environment from requirements only.

The environment included:

```text
VM workloads
storage accounts
virtual networks
web applications
business-critical data
a small operations team
strict recovery expectations
```

The goal was to make the environment observable and recoverable.

## Business Requirements

The design had to satisfy:

```text
1. Platform logs must be queryable centrally.
2. Resource metrics must be reviewed for performance and availability.
3. Failed administrative operations must be searchable.
4. High CPU must trigger an alert.
5. Failed operations in logs must trigger an alert.
6. Resource deletion must trigger an alert.
7. The operations team must receive alert notifications.
8. Alert notifications must be suppressible during planned maintenance.
9. VM performance and dependencies must be monitored.
10. Storage account performance and availability must be monitored.
11. Network connectivity must be monitored over time.
12. NSG filtering and route paths must be troubleshootable.
13. Azure VMs must be backed up.
14. Backup schedule and retention must be defined.
15. Single-file restore must be possible.
16. Whole-VM restore must be possible.
17. Regional disaster recovery must be considered.
18. DR must be testable without impacting production.
19. Backup reporting and alerting must be available.
```

## Target Architecture

```text
Azure resources
   |
   +--> Metrics
   |
   +--> Diagnostic settings
          |
          v
   Log Analytics workspace
          |
          v
   KQL queries / log search alerts

Alerts
   |
   +--> Metric alert
   +--> Log search alert
   +--> Activity log alert
          |
          v
      Action group
          |
          v
      Email / webhook / automation

Maintenance window
   |
   v
Alert processing rule suppresses notifications

Protection
   |
   +--> Recovery Services vault
   |      ├── Backup policy
   |      ├── VM backup
   |      ├── Recovery points
   |      └── Restore operations
   |
   +--> Site Recovery
          ├── Replication
          ├── Test failover
          └── Failover
```

## Monitoring Architecture

| Requirement | Azure feature | Reason |
|---|---|---|
| Central log querying | Log Analytics workspace | Stores and queries logs using KQL. |
| Send resource logs to workspace | Diagnostic settings | Sends platform/resource logs and metrics to destinations. |
| Numeric performance review | Azure Monitor metrics | Metrics show numeric time-series data. |
| Failed operations searchable | AzureActivity / logs in Log Analytics | Failed administrative operations can be queried. |
| VM performance/dependencies | VM insights | Provides prebuilt VM monitoring. |
| Storage performance/availability | Storage insights / metrics | Shows transactions, latency, availability, and errors. |
| Network path troubleshooting | Network Watcher | Provides IP flow verify, Next hop, effective routes/rules. |
| Ongoing connectivity | Connection Monitor | Tracks connectivity over time. |

## Alerting Architecture

| Requirement | Azure feature | Reason |
|---|---|---|
| Alert on high CPU | Metric alert | CPU is a numeric metric. |
| Alert on failed log events | Log search alert | Uses KQL query result. |
| Alert on resource deletion | Activity log alert | Deletion is a management-plane event. |
| Notify operations team | Action group | Defines email/webhook/automation notification target. |
| Suppress alerts during maintenance | Alert processing rule | Suppresses or modifies alert notifications. |

## Backup Architecture

| Requirement | Azure feature | Reason |
|---|---|---|
| Protect Azure VM | Azure Backup | Recovers from deletion/corruption. |
| Store VM backup configuration | Recovery Services vault | Common vault for Azure VM backup. |
| Define schedule and retention | Backup policy | Controls backup frequency and retention. |
| Recover one file | File recovery | Restores selected files from VM backup. |
| Recover whole VM | Restore VM / restore disks | Restores full VM or disks from recovery point. |
| Central backup visibility | Backup reports | Provides reporting across backup estate. |

## Disaster Recovery Architecture

| Requirement | Azure feature | Reason |
|---|---|---|
| Regional disaster recovery | Azure Site Recovery | Replicates workloads for failover. |
| Validate DR safely | Test failover | Tests recovery without impacting production. |
| Actual DR event | Failover | Moves workload to recovery region/site. |
| Accept failover result | Commit | Commits the failover. |
| Reverse protection | Re-protect | Starts protection in the reverse direction. |

## Objective Mapping

This lab covered:

- Interpret metrics in Azure Monitor
- Configure log settings in Azure Monitor
- Query and analyze logs in Azure Monitor
- Set up alert rules, action groups, and alert processing rules
- Configure and interpret monitoring of VMs, storage accounts, and networks by using Azure Monitor Insights
- Use Azure Network Watcher and Connection Monitor
- Create a Recovery Services vault
- Create an Azure Backup vault / compare Backup vault use
- Create and configure a backup policy
- Perform backup and restore operations using Azure Backup
- Configure Azure Site Recovery for Azure resources
- Perform a failover to a secondary region using Site Recovery
- Configure and interpret reports and alerts for backups

## Exam Patterns Learned

| Exam wording | Correct thinking |
|---|---|
| Query logs with KQL | Log Analytics workspace |
| Send resource logs somewhere | Diagnostic settings |
| Alert on CPU threshold | Metric alert |
| Alert from KQL result | Log search alert |
| Alert on resource deletion | Activity log alert |
| Notify operations team | Action group |
| Suppress maintenance alerts | Alert processing rule |
| VM dependency/performance monitoring | VM insights |
| Ongoing connectivity monitoring | Connection Monitor |
| Check NSG allow/deny | IP flow verify |
| Check route path | Next hop |
| Protect VM from data loss | Azure Backup |
| Define backup schedule/retention | Backup policy |
| Recover one file | File recovery |
| Regional DR/failover | Azure Site Recovery |
| Validate DR safely | Test failover |
| Central backup visibility | Backup reports |

## Final Challenge Answer

```text
CPU alert: Azure Monitor metric alert + action group
Deleted file: Azure Backup file recovery from Recovery Services vault
Regional disaster: Azure Site Recovery with replication and failover
```

## Final Mental Model

```text
Metrics show numbers.
Logs show events.
Diagnostic settings send data.
Log Analytics stores/query logs.
KQL asks questions of logs.
Metric alerts detect metric thresholds.
Log search alerts detect KQL results.
Activity log alerts detect control-plane events.
Action groups notify or trigger automation.
Alert processing rules suppress or modify notifications.
Backup restores.
Site Recovery fails over.
Test failover validates.
Backup reports show protection health.
```
