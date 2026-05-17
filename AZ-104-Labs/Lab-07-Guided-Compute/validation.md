# Lab 07 Validation

## Resource Foundation

| Requirement | Status |
|---|---|
| Dedicated compute resource group created | Completed |
| Compute VNet created or reviewed | Completed |
| VM subnet created | Completed |
| VMSS subnet created | Completed |
| Container subnet created or reviewed | Completed |
| App Service integration subnet created or reviewed | Completed |

## Virtual Machine Validation

| Requirement | Status |
|---|---|
| VM created or reviewed | Completed |
| VM NIC, subnet, and IP configuration understood | Completed |
| VM size reviewed | Completed |
| Resize concept understood | Completed |
| OS disk reviewed | Completed |
| Data disk attached or reviewed | Completed |
| Disk caching reviewed | Completed |
| Encryption at host concept reviewed | Completed |
| Availability zone vs availability set explained | Completed |
| VM move concepts and limitations reviewed | Completed |

## VM Scale Set Validation

| Requirement | Status |
|---|---|
| VMSS created or reviewed | Completed |
| Instance count understood | Completed |
| Autoscale rule concept reviewed | Completed |
| Min/default/max instance limits understood | Completed |
| VMSS vs standalone VM decision understood | Completed |

## Container Validation

| Requirement | Status |
|---|---|
| Azure Container Registry created or reviewed | Completed |
| ACR purpose understood | Completed |
| Azure Container Instance deployed or reviewed | Completed |
| ACI sizing concept reviewed | Completed |
| Azure Container Apps deployed or reviewed | Completed |
| Container Apps ingress/revision/scaling concept understood | Completed |
| ACI vs Container Apps distinction understood | Completed |

## App Service Validation

| Requirement | Status |
|---|---|
| App Service plan created or reviewed | Completed |
| App Service app created or reviewed | Completed |
| Scale up vs scale out understood | Completed |
| Deployment slot created or reviewed | Completed |
| Custom domain mapping reviewed | Completed |
| TLS certificate binding reviewed | Completed |
| VNet integration reviewed | Completed |
| Private endpoint for App Service reviewed | Completed |
| App Service backup reviewed | Completed |

## ARM/Bicep Validation

| Requirement | Status |
|---|---|
| ARM/Bicep purpose understood | Completed |
| Parameters and variables reviewed | Completed |
| Dependencies reviewed | Completed |
| Group deployment pattern reviewed | Completed |
| Export template / convert to Bicep concept reviewed | Completed |

## Exam-Readiness Validation

The lab is complete when these statements can be explained without notes:

- VM is for full OS control.
- VM size controls CPU, memory, throughput, disk support, and cost.
- Data disks provide persistent workload storage.
- ReadOnly host caching is commonly suited to read-heavy workloads.
- Encryption at host differs from customer-managed disk encryption with Disk Encryption Set.
- Availability zones and availability sets solve different resiliency problems.
- VMSS is for autoscaling groups of similar VM instances.
- ACR stores private container images.
- ACI runs simple containers quickly.
- Container Apps provides managed scalable container application hosting.
- App Service plan controls App Service compute and scaling.
- Deployment slots support staged deployment and swap.
- VNet integration is App Service outbound private network access.
- Private endpoint is App Service inbound private access.
- ARM/Bicep provides repeatable deployment.

## Completion Statement

Lab 07 is complete because the main AZ-104 compute deployment and configuration patterns were implemented or reviewed and mapped to exam-style feature-selection decisions.
