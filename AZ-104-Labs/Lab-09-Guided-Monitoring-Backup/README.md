# Lab 09 — Guided Monitoring, Backup, and Recovery Lab

**Certification:** Microsoft AZ-104: Azure Administrator Associate  
**Domain:** Monitor and maintain Azure resources  
**Lab type:** Guided practice / architecture-first implementation  
**Status:** Completed  
**Difficulty:** Harder-than-standard guided lab

## Purpose

This lab documents the operational layer of Azure administration: monitoring, alerting, backup, restore, and disaster recovery.

The purpose was to understand how Azure answers four operational questions:

```text
1. What is happening right now?
2. What happened historically?
3. Who should be alerted?
4. Can we recover if something fails?
```

## Architecture Summary

```text
Resource Group: rg-az104-lab09-monitoring

Operational data layer
├── Log Analytics workspace
├── Diagnostic settings
├── Activity logs
├── Resource logs
└── KQL queries

Alerting layer
├── Metric alert
├── Log search alert
├── Activity log alert
├── Action group
└── Alert processing rule

Insights/troubleshooting layer
├── VM insights
├── Storage insights
├── Network Watcher
├── Connection Monitor
├── IP flow verify
└── Next hop

Protection layer
├── Recovery Services vault
├── Backup vault
├── Backup policy
├── Recovery points
├── Restore operations
└── Backup reports/alerts

Disaster recovery layer
├── Azure Site Recovery
├── Replication
├── Recovery plan
├── Test failover
└── Failover
```

## Monitoring Mental Model

| Requirement | Azure feature |
|---|---|
| View numeric performance over time | Metrics |
| Collect detailed logs/events | Diagnostic settings + Log Analytics |
| Query logs | KQL |
| Alert on CPU/availability/numeric threshold | Metric alert |
| Alert from KQL result | Log search alert |
| Alert on resource create/delete/change | Activity log alert |
| Notify people or trigger automation | Action group |
| Suppress alerts during maintenance | Alert processing rule |
| VM performance/dependency monitoring | VM insights |
| Storage performance/availability | Storage insights / metrics |
| Network troubleshooting | Network Watcher |
| Ongoing connectivity monitoring | Connection Monitor |

## Backup and Recovery Mental Model

| Requirement | Azure feature |
|---|---|
| Protect Azure VM from deletion/corruption | Azure Backup |
| Store VM backup configuration and recovery points | Recovery Services vault |
| Newer Azure backup workload vault type | Backup vault |
| Define schedule and retention | Backup policy |
| Restore one or more files | File recovery |
| Restore entire VM | Restore VM / restore disks |
| Regional disaster recovery/failover | Azure Site Recovery |
| Validate DR safely | Test failover |
| Actual DR event | Failover |
| Central backup visibility | Backup reports |

## AZ-104 Objectives Covered

### Monitor resources in Azure

- Interpreted metrics in Azure Monitor
- Configured log settings through diagnostic settings
- Queried and analyzed logs in Log Analytics using KQL
- Set up alert rules, action groups, and alert processing rules
- Reviewed monitoring of VMs, storage accounts, and networks with Azure Monitor Insights
- Reviewed Network Watcher and Connection Monitor

### Implement backup and recovery

- Created or reviewed Recovery Services vault
- Created or reviewed Backup vault
- Created and configured backup policy
- Performed or reviewed Azure Backup and restore operations
- Configured or reviewed Azure Site Recovery for Azure resources
- Reviewed failover to a secondary region using Site Recovery
- Configured or interpreted backup reports and alerts

## Implementation Summary

Completed or reviewed tasks:

- Created dedicated monitoring resource group
- Created Log Analytics workspace
- Configured diagnostic settings concept
- Interpreted Azure Monitor metrics
- Queried logs with KQL
- Created/reviewed action group
- Created/reviewed metric alert
- Created/reviewed log search alert
- Created/reviewed activity log alert
- Created/reviewed alert processing rule
- Enabled/reviewed VM insights
- Reviewed storage monitoring/insights
- Reviewed Network Watcher and Connection Monitor
- Created/reviewed Recovery Services vault
- Created/reviewed Backup vault
- Created/reviewed backup policy
- Reviewed Azure VM backup
- Reviewed file recovery and VM restore options
- Reviewed Azure Site Recovery
- Reviewed test failover vs failover
- Reviewed backup reports and alerts

## Key Architecture Lessons

### Metrics vs Logs

```text
Metrics = numeric time-series performance data
Logs = detailed records/events that can be queried
```

Use metrics for simple numeric thresholds. Use logs/KQL for detailed event analysis.

### Diagnostic Settings

Diagnostic settings decide where Azure sends resource logs and metrics.

Common destinations:

```text
Log Analytics workspace
Storage account
Event Hub
Partner solution
```

### Alerts

```text
Metric alert = numeric threshold
Log search alert = KQL query result
Activity log alert = management-plane event
Action group = notification/automation target
Alert processing rule = suppress/modify alert notifications
```

### Azure Backup vs Azure Site Recovery

```text
Azure Backup = recover data/VM state after deletion/corruption
Azure Site Recovery = replicate/fail over workloads for disaster recovery
```

### Restore vs Failover

```text
Restore = recover from backup/recovery point
Test failover = validate DR without affecting production
Failover = actual disaster recovery action
```

## Exam Patterns Reinforced

| Exam wording | Correct thinking |
|---|---|
| Query logs with KQL | Log Analytics workspace |
| Send resource logs to workspace | Diagnostic settings |
| Alert on CPU above threshold | Metric alert |
| Alert from custom query | Log search alert |
| Alert when resource is deleted | Activity log alert |
| Notify ops team | Action group |
| Suppress alerts during maintenance | Alert processing rule |
| Monitor VM dependencies/performance | VM insights |
| Monitor connectivity over time | Connection Monitor |
| Check NSG allow/deny | IP flow verify |
| Check route path | Next hop |
| Protect VM from corruption/deletion | Azure Backup |
| Define backup schedule/retention | Backup policy |
| Recover a single file | File recovery |
| Regional failover | Azure Site Recovery |
| Validate DR safely | Test failover |
| View backup health centrally | Backup reports |

## Final Mental Model

```text
Metrics = numeric performance data.
Logs = detailed records/events.
Diagnostic settings = send logs/metrics somewhere.
Log Analytics = store/query logs.
KQL = query logs.
Metric alert = numeric threshold alert.
Log search alert = KQL-based alert.
Activity log alert = management event alert.
Action group = who/what gets notified.
Alert processing rule = suppress/modify alert notifications.
VM insights = VM performance/dependency monitoring.
Storage insights = storage health/performance visibility.
Network Watcher = network troubleshooting tools.
Connection Monitor = ongoing connectivity monitoring.
Recovery Services vault = VM backup / ASR common vault.
Backup vault = newer backup workload vault type.
Backup policy = schedule + retention.
Recovery point = restore point.
Azure Backup = recover from deletion/corruption.
Azure Site Recovery = failover/disaster recovery.
Test failover = safe DR validation.
Failover = actual DR event.
Backup reports = central backup visibility.
```
