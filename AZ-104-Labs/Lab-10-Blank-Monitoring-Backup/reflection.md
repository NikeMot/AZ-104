# Lab 10 Reflection

## What this lab proved

This lab proved that monitoring, alerting, backup, restore, and disaster recovery decisions can be made from requirements without hand-holding.

The main skill was converting operational requirements into the correct Azure feature.

## Metrics vs Logs

Metrics are numeric time-series values.

Logs are detailed event records.

```text
Metrics = numbers over time
Logs = events and details
```

## Diagnostic Settings vs Alerts

Diagnostic settings send logs and metrics to destinations.

Alerts evaluate conditions and notify or trigger actions.

```text
Diagnostic settings = data routing
Alerts = condition detection
```

## Alert Type Selection

```text
CPU threshold = metric alert
KQL query result = log search alert
Resource deletion = activity log alert
```

## Action Group vs Alert Processing Rule

An action group defines who or what gets notified when an alert fires.

An alert processing rule suppresses or modifies alert notifications.

```text
Action group = notify/trigger
Alert processing rule = suppress/modify
```

## VM Insights vs Network Watcher

VM insights is for VM performance and dependency monitoring.

Network Watcher is for network troubleshooting.

```text
VM performance/dependency = VM insights
NSG allow/deny = IP flow verify
Route path = Next hop
Ongoing connectivity = Connection Monitor
```

## Azure Backup vs Azure Site Recovery

Azure Backup restores data or VM state after deletion, corruption, or loss.

Azure Site Recovery replicates workloads for disaster recovery and failover.

```text
Backup = restore
Site Recovery = failover
```

## File Recovery vs VM Restore

```text
One file = file recovery
Whole VM = restore VM
Safe inspection copy = restore as new VM or restore disks
```

## Test Failover vs Failover

Test failover validates disaster recovery without affecting production.

Failover is the real disaster recovery action.

```text
Test failover = safe validation
Failover = actual recovery event
```

## Recovery Services Vault vs Backup Vault

Recovery Services vault is commonly used for Azure VM backup and Azure Site Recovery scenarios.

Backup vault is used for newer Azure Backup workloads where that vault type is required.

The exam clue is usually in the workload type.

## What would change in production

A production design would include:

```text
centralized Log Analytics workspace design
data retention standards
diagnostic settings policy enforcement
standard alert rule baselines
action group escalation paths
maintenance suppression process
backup policy tiers
regular restore testing
regular DR test failovers
backup report review cadence
runbooks for incident response
```

## Exam readiness judgement

This lab strengthens AZ-104 readiness because the exam often asks:

```text
Which monitoring data type should be used?
Which alert type fits the condition?
How should notifications be sent or suppressed?
Which tool diagnoses a network issue?
Is this backup/restore or disaster recovery?
Should the action be file recovery, VM restore, test failover, or failover?
```

The domain is ready when those distinctions are automatic.

## Final memory cue

```text
Metrics show numbers.
Logs show events.
Diagnostic settings send data.
Log Analytics stores/query logs.
KQL asks questions of logs.
Metric alerts detect metric thresholds.
Log search alerts detect KQL results.
Activity log alerts detect management events.
Action groups notify.
Alert processing rules suppress.
Backup restores.
Site Recovery fails over.
Test failover validates.
Backup reports show protection health.
```
