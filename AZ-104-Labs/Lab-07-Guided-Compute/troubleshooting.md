# Lab 07 Troubleshooting Notes

## Troubleshooting Approach

Azure compute troubleshooting depends on identifying which layer is failing:

```text
Deployment layer
Compute resource layer
Networking layer
Disk/storage layer
Guest OS/application layer
Scaling layer
Platform feature layer
```

## VM Cannot Be Reached

Check:

```text
VM power state
NIC private IP
Public IP or Bastion/private access path
NSG rules
Route table if applicable
Guest OS firewall
SSH/RDP service state
Credentials or login method
```

Exam lesson:

```text
A VM existing in Azure does not guarantee it is reachable. Access depends on network path, NSG, route, guest OS, and credentials.
```

## VM Resize Fails

Check:

```text
Target size availability in region
Quota limits
VM family availability
Whether VM must be deallocated
Disk/network compatibility
Availability set or zone constraints
```

Exam lesson:

```text
Resize changes compute capacity, but it may be constrained by region, quota, cluster, or availability configuration.
```

## Data Disk Not Visible Inside OS

Check:

```text
Disk is attached in Azure
Correct LUN assigned
Guest OS detects the disk
Disk is initialized
Disk is partitioned/formatted
Disk is mounted or assigned a drive letter
```

Exam lesson:

```text
Attaching a disk in Azure is not always enough. The guest OS may still need initialization and mounting.
```

## VMSS Does Not Scale Out

Check:

```text
Autoscale profile enabled
Metric threshold reached
Scale-out rule exists
Min/default/max instance limits
CPU metric availability
Subscription quota
Cooldown period
```

Exam lesson:

```text
Autoscale requires valid rules, available quota, and metrics crossing thresholds.
```

## Container Instance Not Reachable

Check:

```text
Container state
Image pull succeeded
Port exposed
Public IP or DNS label assigned if public access required
Container process listening on target port
CPU/memory allocation sufficient
```

Exam lesson:

```text
ACI is simple, but image, port, network, and container process must all be correct.
```

## Container App Not Reachable

Check:

```text
Ingress enabled
External vs internal ingress setting
Target port correct
Revision is active
Container health/probe status
Scale settings allow at least one active replica if needed
Image pull succeeded
```

Exam lesson:

```text
Container Apps adds managed ingress, revisions, and scaling. Troubleshooting includes both container health and platform routing.
```

## App Service App Not Working

Check:

```text
App Service plan is running and supports the required feature
Runtime stack is correct
Application settings are correct
Deployment succeeded
Logs enabled/reviewed
Custom domain DNS points correctly
TLS binding exists if HTTPS required
Access restrictions are not blocking traffic
```

Exam lesson:

```text
App Service removes OS management, but plan tier, runtime, app settings, DNS, TLS, and networking still matter.
```

## Deployment Slot Swap Problem

Check:

```text
Slot exists
App is deployed to correct slot
Slot-specific settings are marked correctly
Warm-up behavior
Swap direction
Custom domains and certificates if relevant
Production and staging settings differences
```

Exam lesson:

```text
Deployment slots are for staged release and rollback. Slot-sticky settings prevent environment-specific values from swapping accidentally.
```

## App Service Networking Issue

Check:

```text
Outbound to VNet required? Use VNet integration.
Inbound private access required? Use private endpoint.
Public inbound restriction required? Use access restrictions.
DNS resolution required? Check custom DNS/VNet DNS settings.
```

Exam lesson:

```text
VNet integration is outbound from App Service. Private endpoint is inbound private access to App Service.
```

## ARM/Bicep Deployment Fails

Check:

```text
Resource provider registered
Template syntax valid
Parameters provided
Resource names unique where required
Dependencies correct
Location supports resource type/SKU
Permissions sufficient
Quota available
```

Exam lesson:

```text
Bicep/ARM deployments fail from syntax, parameters, dependency, permissions, region/SKU, or quota issues.
```

## Compute Feature Selection Troubleshooting

| Problem | Likely feature |
|---|---|
| Need full OS control | VM |
| Need autoscaling identical VMs | VMSS |
| Need simple one-off container | ACI |
| Need managed scalable container app | Container Apps |
| Need private container image store | ACR |
| Need managed web hosting | App Service |
| Need staged App Service release | Deployment slots |
| Need repeatable deployment | ARM/Bicep |

## Final Troubleshooting Memory Cue

```text
VM issue? Check power, NIC, NSG, route, guest OS.
Disk issue? Check attach, LUN, initialize, mount.
Scale issue? Check rule, metric, quota, limits.
Container issue? Check image, ingress, port, health.
App Service issue? Check plan, runtime, deployment, DNS, TLS, networking.
Bicep issue? Check syntax, parameters, dependencies, region, permissions.
```
