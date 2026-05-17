# Lab 07 Reflection

## What this lab reinforced

This lab reinforced that Azure compute is not one service. It is a set of workload hosting choices.

The key skill is choosing the correct compute option from requirements:

```text
VM = full OS control
VMSS = autoscaling similar VMs
ACI = simple container
Container Apps = managed scalable container app
ACR = private image registry
App Service = managed web hosting
ARM/Bicep = repeatable deployment
```

## Main architecture lesson

The compute layer should match the workload.

Not every workload belongs on a VM. Not every container needs AKS. Not every web app needs infrastructure-level control.

The best Azure administrator chooses the simplest compute platform that meets the requirement without adding unnecessary management overhead.

## Most important decisions

1. Use VMs when OS-level control is required.
2. Use managed disks for VM storage.
3. Use VM resize for CPU/memory changes.
4. Use data disks for persistent workload data.
5. Use ReadOnly host caching for appropriate read-heavy data disk scenarios.
6. Use encryption at host when host-level encryption is required.
7. Use availability zones for zone/datacenter resiliency.
8. Use availability sets for fault/update domain resiliency.
9. Use VMSS for autoscaling groups of similar VM instances.
10. Use ACR for private container images.
11. Use ACI for simple container execution.
12. Use Container Apps for managed container applications with scaling/revisions.
13. Use App Service for managed web hosting.
14. Use App Service plan for scaling and compute tier control.
15. Use deployment slots for staged deployment and rollback.
16. Use VNet integration for App Service outbound access to private resources.
17. Use private endpoint for private inbound access to App Service.
18. Use ARM/Bicep for repeatable deployments.

## Concepts that matter most for AZ-104

### VM vs App Service

A VM gives more control but more responsibility.

App Service gives less OS control but reduces management overhead.

```text
Need OS control? VM.
Need managed web hosting? App Service.
```

### Availability zone vs availability set

```text
Availability zone = datacenter/zone failure protection.
Availability set = rack/update-domain failure protection.
```

### VMSS vs availability set

An availability set protects multiple VMs from hardware/update-domain failures.

A VM Scale Set manages a scalable group of similar VM instances.

```text
Need resiliency for manually managed VMs? Availability set.
Need autoscaling identical instances? VMSS.
```

### ACI vs Container Apps

```text
ACI = run a simple container quickly.
Container Apps = managed container app with ingress, scaling, and revisions.
```

### App Service networking

```text
Outbound from App Service to VNet = VNet integration.
Inbound private access to App Service = Private endpoint.
Restrict public inbound = Access restrictions.
```

### App Service slots

Deployment slots reduce release risk.

```text
Deploy to staging -> test -> swap to production.
```

## Review items

- Continue reviewing VMSS autoscale rules.
- Continue reviewing App Service plan tiers and feature availability.
- Continue reviewing VNet integration vs private endpoint for App Service.
- Continue reviewing deployment slots and slot-sticky settings.
- Continue reviewing ARM/Bicep dependencies and parameters.
- Continue reviewing encryption at host vs Disk Encryption Set.

## Readiness judgement

This lab provides strong readiness for the AZ-104 compute domain if these feature-selection decisions are automatic:

```text
VM or App Service?
Availability zone or availability set?
VMSS or standalone VM?
ACI or Container Apps?
VNet integration or private endpoint?
Deployment slot or direct deployment?
ARM/Bicep or portal?
```

The domain is ready when the answer can be chosen from the wording of the requirement.
