# Lab 10 Troubleshooting Notes

## KQL Query Returns No Data

Check:

```text
Diagnostic settings enabled
Correct workspace selected
Correct table queried
Correct time range selected
Data ingestion delay considered
Agent configured if table requires it
Resource actually generating logs
```

Exam lesson:

```text
KQL can only query data that has been collected into the workspace.
```

## Diagnostic Logs Missing

Check:

```text
Diagnostic setting exists
Correct log categories selected
Destination is Log Analytics workspace
Correct workspace selected
Resource supports the selected category
Enough time for ingestion
```

Exam lesson:

```text
Diagnostic settings send resource logs and metrics to destinations. They are not alert rules.
```

## Metric Alert Not Firing

Check:

```text
Correct resource scope
Correct metric selected
Correct aggregation
Threshold reached
Evaluation frequency/window
Alert enabled
Action group attached if notification expected
```

Exam lesson:

```text
Metric alerts depend on the metric, aggregation, threshold, scope, and evaluation window.
```

## Log Search Alert Not Firing

Check:

```text
KQL query returns results manually
Correct workspace scope
Correct threshold
Correct evaluation frequency
Correct time range
Alert enabled
Action group attached
```

Exam lesson:

```text
If the KQL query returns no results, the log search alert will not fire.
```

## Activity Log Alert Not Firing

Check:

```text
Correct subscription/resource group scope
Correct event category
Correct operation name
Correct status filter
Alert enabled
Action group attached
```

Exam lesson:

```text
Activity log alerts monitor control-plane events such as resource deletion, create/update actions, and service health events.
```

## Action Group Not Notifying

Check:

```text
Alert rule fired
Action group attached to alert rule
Receiver configured correctly
Email/SMS/webhook confirmed
Alert processing rule did not suppress notification
Notification destination reachable
```

Exam lesson:

```text
Alert condition and alert notification are separate. Action groups handle notification/action.
```

## Alert Suppressed Unexpectedly

Check:

```text
Alert processing rule scope
Suppression schedule
Rule enabled state
Target alert rules/resources
Maintenance window configuration
```

Exam lesson:

```text
Alert processing rules can suppress notifications even when the alert itself fires.
```

## VM Insights Missing Data

Check:

```text
VM insights enabled
Agent/extension installed
Workspace selected
VM running
Data collection rule/agent configured where required
Time range long enough
```

## Connection Monitor Reports Failure

Check:

```text
Source endpoint
Destination endpoint
Port/protocol
DNS resolution
NSG rules
Route path
Target service listening
Guest OS firewall
```

Exam lesson:

```text
Connection Monitor detects reachability over time, but root cause can be DNS, routing, NSG, or service health.
```

## VM Backup Fails

Check:

```text
Backup job error details
Recovery Services vault region/support
Backup policy assigned
VM supported
VM extension health
Permissions
Network restrictions if relevant
```

Exam lesson:

```text
Always inspect the backup job error before guessing.
```

## Restore Option Is Unclear

Ask:

```text
Need one file?
Need entire VM?
Need a safe inspection copy?
Need to replace original disks?
```

Decision table:

| Requirement | Restore choice |
|---|---|
| One file | File recovery |
| Whole VM | Restore VM |
| Safe inspection copy | Restore as new VM or restore disks |
| Replace original | Restore/replace disk pattern |

## Site Recovery Replication Fails

Check:

```text
Source VM supported
Target region selected
Target VNet/resource group configured
Replication policy configured
Vault configured
Replication health
Network mapping
Storage/cache configuration
```

Exam lesson:

```text
ASR is for replication and failover, not ordinary file restore.
```

## Test Failover Confusion

| Requirement | Correct action |
|---|---|
| Validate DR safely | Test failover |
| Actual disaster recovery event | Failover |
| Accept failover result | Commit |
| Protect reverse direction | Re-protect |

## Backup Reports Missing Data

Check:

```text
Reporting configured
Workspace configured if required
Vault selected
Protected items exist
Jobs have run
Filters/time range correct
Data ingestion delay considered
```

## Final Troubleshooting Memory Cue

```text
No logs? Check diagnostic settings, workspace, table, time range.
No alert? Check condition, scope, action group, processing rule.
No notification? Check action group and suppression rules.
Backup issue? Check vault, policy, job error, VM support.
Restore issue? Clarify file, VM, disk, or copy.
DR issue? Check ASR replication, test failover, failover state.
```
