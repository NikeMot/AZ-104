# Lab 08 Troubleshooting Notes

## VM Cannot Be Reached

Check:

```text
VM power state
NIC and IP configuration
Public IP or Bastion/private access path
NSG rules
Route table if applicable
Guest OS firewall
SSH/RDP service status
Credentials or login permissions
```

Exam lesson:

```text
VM access depends on compute state, network path, NSG, route, guest OS, and credentials.
```

## VM Resize Fails

Check:

```text
Target size exists in region
Quota is sufficient
VM family is available
Availability set/zone constraints
VM may need deallocation
Disk/network compatibility
```

Exam lesson:

```text
Resize changes VM capacity but can be blocked by SKU, region, quota, or allocation constraints.
```

## Data Disk Not Visible Inside OS

Check:

```text
Disk is attached in Azure
Correct LUN assigned
Guest OS detects disk
Disk is initialized
Disk is partitioned/formatted
Disk is mounted or assigned a drive letter
```

Exam lesson:

```text
Azure attachment and guest OS usability are separate steps.
```

## VMSS Does Not Scale Out

Check:

```text
Autoscale profile enabled
Scale-out rule exists
Metric threshold reached
Cooldown period
Min/default/max limits
Quota available
Instance health
```

Exam lesson:

```text
Autoscale requires valid rules, metrics, limits, and quota.
```

## Container Image Pull Fails

Check:

```text
Image name and tag correct
ACR exists
Authentication configured
Managed identity or registry credentials valid
Network restrictions not blocking pull
Image exists in registry
```

Exam lesson:

```text
ACR stores images, but runtimes need permission and network access to pull them.
```

## ACI Container Not Reachable

Check:

```text
Container state
Image pull succeeded
Port exposed
DNS label/public IP if public access required
Container process listening
CPU/memory sufficient
```

Exam lesson:

```text
ACI is simple, but image, port, network, and process health still matter.
```

## Container App Not Reachable

Check:

```text
Ingress enabled
External/internal ingress setting
Target port correct
Revision active
Container health
Replica count
Image pull succeeded
```

Exam lesson:

```text
Container Apps adds ingress, revisions, and scale behavior on top of the container.
```

## App Service Custom Domain Fails

Check:

```text
DNS record type correct
DNS target correct
Domain ownership validated
Record propagation complete
Custom domain added to correct app
```

Exam lesson:

```text
Custom domain requires correct DNS and ownership validation.
```

## TLS Binding Fails

Check:

```text
Certificate uploaded/imported/managed certificate created
Certificate matches hostname
Custom domain added first
Certificate not expired
Binding created for hostname
HTTPS-only if required
```

Exam lesson:

```text
DNS maps the name; TLS secures the name.
```

## Deployment Slot Swap Issue

Check:

```text
Slot exists
Correct app deployed to staging slot
Slot-specific settings marked correctly
Warm-up works
Swap direction correct
Custom domains/certificates considered
Production/staging settings reviewed
```

Exam lesson:

```text
Deployment slots are for staged release and rollback, not scaling.
```

## App Service Networking Confusion

| Requirement | Correct feature |
|---|---|
| App Service needs outbound access to VNet/private resources | VNet integration |
| Clients need private inbound access to App Service | Private endpoint |
| Restrict public inbound traffic | Access restrictions |

Exam lesson:

```text
VNet integration is outbound. Private endpoint is inbound.
```

## ARM/Bicep Deployment Failure

Check:

```text
Template syntax
Parameters provided
Resource names unique
Dependencies correct
Resource provider registered
SKU available in region
Permissions sufficient
Quota available
```

Exam lesson:

```text
IaC failures often come from parameters, dependencies, provider registration, SKU availability, or permissions.
```

## Final Troubleshooting Memory Cue

```text
VM issue? Power, NIC, NSG, route, guest OS.
Disk issue? Attach, LUN, initialize, mount.
Scale issue? Rule, metric, quota, limits.
Container issue? Image, registry, ingress, port, health.
App Service issue? Plan, runtime, deployment, DNS, TLS, networking.
Bicep issue? Syntax, parameters, dependencies, region, permissions.
```
