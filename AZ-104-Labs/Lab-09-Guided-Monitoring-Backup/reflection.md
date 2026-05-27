# Lab 09 Reflection

## What this lab reinforced

This lab reinforced that monitoring and recovery are about operational visibility and resilience.

The key questions are:

```text
What is happening?
What happened?
Who needs to know?
Can we recover?
Can we fail over if the region/service fails?
```

## Metrics vs Logs

Metrics are numeric performance data over time.

Logs are detailed records and events.

```text
Metrics = numbers
Logs = events/details
```

## Diagnostic Settings

Diagnostic settings are the bridge between Azure resources and monitoring destinations.

They send logs and metrics to destinations such as:

```text
Log Analytics workspace
Storage account
Event Hub
Partner solution
```

## Log Analytics and KQL

Log Analytics stores logs.

KQL queries those logs.

```text
Need to query logs = Log Analytics + KQL
```

## Alerts

The alerting model is:

```text
Alert rule detects condition
Action group notifies or triggers automation
Alert processing rule can suppress or modify notifications
```

Important distinctions:

```text
Metric alert = numeric threshold
Log search alert = KQL result
Activity log alert = management-plane event
```

## Insights and Network Watcher

Insights provide prebuilt monitoring views.

Network Watcher provides network troubleshooting tools.

```text
VM insights = VM performance/dependencies
Storage insights = storage performance/availability
Connection Monitor = ongoing connectivity
IP flow verify = NSG allow/deny
Next hop = route path
```

## Azure Backup vs Azure Site Recovery

Azure Backup and Site Recovery solve different problems.

```text
Azure Backup = recover deleted/corrupted data or VM state
Azure Site Recovery = disaster recovery and regional failover
```

This is one of the most important exam distinctions in the monitoring/maintenance domain.

## Restore vs Failover

Restore comes from backup recovery points.

Failover comes from disaster recovery replication.

```text
Recover one file = file recovery
Recover whole VM = restore VM
Validate DR safely = test failover
Actual DR event = failover
```

## Most important decisions

1. Use metrics for simple numeric thresholds.
2. Use logs/KQL for detailed event analysis.
3. Use diagnostic settings to send resource logs to a workspace.
4. Use metric alerts for performance thresholds.
5. Use log search alerts for query-based conditions.
6. Use activity log alerts for management-plane events.
7. Use action groups for notification/automation.
8. Use alert processing rules for maintenance suppression.
9. Use VM insights for VM monitoring.
10. Use Connection Monitor for ongoing network reachability.
11. Use Azure Backup for recoverability.
12. Use Azure Site Recovery for regional failover.
13. Use backup reports for central backup visibility.

## Exam readiness judgement

This lab prepares for AZ-104 because monitoring/maintenance questions often ask:

```text
Which monitoring data type should you use?
Which alert type fits the condition?
Where should logs be sent?
Which tool diagnoses the network issue?
Is this a backup/restore problem or a disaster recovery problem?
Should you restore, test failover, or fail over?
```

The domain is ready when those distinctions are automatic.

## Final memory cue

```text
Metrics show numbers.
Logs show events.
Diagnostic settings send data.
Log Analytics stores/query logs.
KQL asks questions of logs.
Alerts detect conditions.
Action groups notify.
Alert processing rules suppress.
Backup restores.
Site Recovery fails over.
Test failover validates.
Backup reports show protection health.
```
