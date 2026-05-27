# Lab 09 Troubleshooting Notes

## Troubleshooting Approach

Monitoring and recovery troubleshooting starts by identifying which layer is failing:

```text
Data collection
Querying
Alert evaluation
Notification delivery
Insight/agent configuration
Backup configuration
Restore operation
Disaster recovery replication/failover
```

## KQL Query Returns No Data

Check:

```text
Diagnostic settings enabled
Correct Log Analytics workspace selected
Correct table queried
Correct time range selected
Data ingestion delay considered
Agent configured if table requires agent data
Resource actually generating logs
```

Exam lesson:

```text
If logs are not collected into the workspace, KQL cannot query them.
```

## Alert Did Not Notify Anyone

Check:

```text
Alert rule fired
Action group attached
Notification receiver configured correctly
Alert processing rule did not suppress notification
Alert rule enabled
Scope and condition correct
Email/SMS/webhook confirmed
```

Exam lesson:

```text
Alert rule detects the condition. Action group sends the notification. Alert processing rule may suppress it.
```

## Metric Alert Not Firing

Check:

```text
Correct resource scope
Correct metric selected
Correct aggregation selected
Threshold actually reached
Evaluation frequency and window configured correctly
Alert rule enabled
Metric data available
```

Exam lesson:

```text
Metric alerts are best for numeric time-series thresholds, but aggregation/window choices matter.
```

## Log Search Alert Not Firing

Check:

```text
KQL query returns expected results manually
Query time range correct
Alert threshold correct
Evaluation frequency correct
Workspace scope correct
Alert enabled
Action group attached
```

Exam lesson:

```text
A log search alert depends on the KQL query returning the expected results within the evaluation window.
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
Activity log alerts monitor management-plane events such as create, delete, update, service health, and administrative operations.
```

## VM Insights Not Showing Data

Check:

```text
VM insights enabled
Agent/extension installed
Workspace selected
VM running
Network/permissions allow data collection
Time range long enough
```

Exam lesson:

```text
Insights depend on data collection being enabled and sent to the correct workspace.
```

## Connection Monitor Shows Failure

Check:

```text
Source and destination correct
Port/protocol correct
NSG rules
Route path
DNS resolution
Target service listening
Guest OS firewall
```

Exam lesson:

```text
Connection Monitor shows ongoing reachability, but you still troubleshoot DNS, route, filtering, and service health separately.
```

## VM Backup Failed

Check:

```text
Backup job error details
VM exists and is supported
Vault region/support
Backup policy assigned
VM extension status
Permissions
Network restrictions if relevant
Resource locks if deletion/cleanup involved
```

Exam lesson:

```text
Always check the backup job error before guessing. VM state alone is not always the root cause.
```

## Restore Requirement Is Unclear

Ask:

```text
Need one file?
Need entire VM?
Need restore as a separate copy?
Need overwrite/replace original?
Need inspect backup safely?
```

Decision table:

| Requirement | Restore option |
|---|---|
| Recover one file | File recovery |
| Restore whole VM separately | Restore as new VM |
| Inspect backup safely | Restore disks or new VM |
| Replace original VM/disk | Replace/restore disk pattern |

## Azure Site Recovery Replication Issue

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
ASR is for disaster recovery replication and failover, not ordinary file restore.
```

## Test Failover vs Failover Confusion

| Requirement | Correct action |
|---|---|
| Validate DR safely | Test failover |
| Actual disaster recovery event | Failover |
| Accept failover result | Commit |
| Protect workload in reverse direction | Re-protect |

## Backup Reports Missing Data

Check:

```text
Reporting configured
Workspace configured if required
Backup data has had time to appear
Vault selected
Filters/time range correct
Backup items protected
```

## Final Troubleshooting Memory Cue

```text
No logs? Check diagnostic settings/workspace/time range.
No alert? Check rule, condition, action group, processing rule.
No backup? Check vault, policy, job error, VM support.
Wrong restore? Clarify file vs VM vs disk vs new copy.
Need DR? Use Site Recovery, not Backup.
Need safe DR validation? Test failover.
```
