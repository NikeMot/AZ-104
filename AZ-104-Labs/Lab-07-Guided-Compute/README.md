# Lab 07 — Guided Compute Architecture Lab

**Certification:** Microsoft AZ-104: Azure Administrator Associate  
**Domain:** Deploy and manage Azure compute resources  
**Lab type:** Guided practice / architecture-first implementation  
**Status:** Completed  
**Difficulty:** Harder-than-standard guided lab

## Purpose

This lab documents the Azure compute architecture patterns required for AZ-104. The purpose was not just to deploy compute resources, but to understand when to choose each Azure compute option and how the components relate to each other.

The lab covered:

- virtual machines
- managed disks
- VM sizing
- disk caching
- encryption at host
- availability zones and availability sets
- VM Scale Sets
- ARM templates and Bicep
- Azure Container Registry
- Azure Container Instances
- Azure Container Apps
- App Service plans
- App Service web apps
- deployment slots
- custom DNS and TLS
- App Service networking
- App Service backup

## Architecture Summary

```text
Resource Group: rg-az104-lab07-compute

VNet: vnet-compute-lab07
├── snet-vm
├── snet-vmss
├── snet-containers
└── snet-appservice-integration

Compute Layer 1 — Virtual Machines
├── vm-web-01
├── OS disk
├── optional data disk
├── VM resize operation
├── disk caching review
└── encryption / availability review

Compute Layer 2 — VM Scale Set
├── vmss-web-lab07
├── multiple similar instances
└── autoscale rules

Compute Layer 3 — Containers
├── Azure Container Registry
├── Azure Container Instance
└── Azure Container Apps

Compute Layer 4 — App Service
├── App Service plan
├── Web App
├── scale-out configuration
├── deployment slot
├── custom DNS/TLS review
├── networking review
└── backup review
```

## Compute Feature Selection

| Requirement | Correct compute feature |
|---|---|
| Full OS control | Virtual Machine |
| More CPU/RAM for a VM | Resize VM |
| Extra persistent VM storage | Managed data disk |
| Read-heavy disk performance | ReadOnly host caching |
| Encrypt VM data at host level | Encryption at host |
| Datacenter-level resiliency | Availability zone |
| Rack/update-domain resiliency | Availability set |
| Autoscaling group of similar VMs | VM Scale Set |
| Repeatable deployment | ARM template or Bicep |
| Private container image storage | Azure Container Registry |
| Simple quick container | Azure Container Instances |
| Managed scalable container app | Azure Container Apps |
| Managed web hosting | Azure App Service |
| App Service compute/scale boundary | App Service plan |
| Blue/green deployment | Deployment slot |
| Friendly app hostname | Custom domain |
| HTTPS for app hostname | TLS certificate binding |
| App outbound access to VNet | VNet integration |
| Private inbound access to App Service | Private endpoint |
| App content/config backup | App Service backup |

## AZ-104 Objectives Covered

### Automate deployment of resources by using ARM templates or Bicep files

- Interpreted ARM/Bicep deployment structure
- Reviewed parameters, variables, dependencies, and deployment scope
- Reviewed deployment using `az deployment group create`
- Reviewed export template and ARM-to-Bicep conversion concept

### Create and configure virtual machines

- Created a virtual machine
- Reviewed encryption at host
- Reviewed moving VMs to another resource group, subscription, or region
- Managed VM sizes
- Managed VM disks
- Reviewed availability zones and availability sets
- Deployed or reviewed VM Scale Sets

### Provision and manage containers

- Created or reviewed Azure Container Registry
- Provisioned or reviewed Azure Container Instances
- Provisioned or reviewed Azure Container Apps
- Reviewed container sizing and scaling

### Create and configure Azure App Service

- Provisioned an App Service plan
- Configured App Service plan scaling
- Created an App Service web app
- Reviewed custom DNS and TLS
- Reviewed App Service backup
- Reviewed App Service networking
- Configured or reviewed deployment slots

## Key Architecture Lessons

### Virtual Machines

VMs are used when the workload requires OS-level control, custom software, legacy application support, or server-style administration.

A VM is not just one resource. It depends on:

```text
VM resource
NIC
VNet/subnet
OS disk
optional data disks
NSG
optional public IP
availability configuration
```

### Managed Disks

Managed disks separate storage from the VM configuration and allow OS and data storage to be managed independently.

Important distinctions:

```text
OS disk = operating system
Data disk = workload/application data
Temporary disk = non-persistent temporary storage
```

### Availability

Availability options solve different failure models:

| Feature | Failure model |
|---|---|
| Availability zone | Datacenter/zone failure |
| Availability set | Fault domain/update domain inside a datacenter |
| VM Scale Set | Scalable group of similar instances |

### Containers

Container service selection:

```text
ACR = stores images
ACI = quick/simple container
Container Apps = managed scalable app container
AKS = Kubernetes orchestration, beyond this lab focus
```

### App Service

App Service is a managed web hosting platform. The App Service plan defines the compute resources, cost tier, available features, and scaling capacity.

Important App Service distinctions:

```text
Scale up = bigger worker/tier
Scale out = more instances
Deployment slot = staging/blue-green deployment
VNet integration = outbound access to VNet
Private endpoint = inbound private access
Custom domain = friendly DNS name
TLS binding = secure HTTPS
```

### ARM/Bicep

ARM and Bicep are used for repeatable deployment. The key exam idea is that infrastructure can be described declaratively and redeployed consistently.

## Implementation Summary

Completed or reviewed tasks:

- Created dedicated compute resource group
- Created compute VNet and subnets
- Created a VM
- Reviewed VM size changes
- Added or reviewed VM data disk configuration
- Reviewed disk caching choices
- Reviewed encryption at host
- Compared availability zones and availability sets
- Reviewed VM move patterns and limitations
- Created or reviewed VM Scale Set
- Reviewed VMSS autoscale rules
- Created or reviewed Azure Container Registry
- Created or reviewed Azure Container Instance
- Created or reviewed Azure Container Apps
- Created App Service plan
- Created App Service web app
- Reviewed App Service scaling
- Created or reviewed deployment slot
- Reviewed custom DNS and TLS
- Reviewed App Service networking
- Reviewed App Service backup
- Reviewed ARM/Bicep deployment pattern

## Exam Patterns Reinforced

| Exam wording | Correct thinking |
|---|---|
| Need full OS control | VM |
| Need more CPU/RAM | Resize VM |
| Need persistent extra storage | Add managed data disk |
| Need read-heavy disk acceleration | ReadOnly host caching |
| Need host-level encryption | Encryption at host |
| Need datacenter-level resiliency | Availability zone |
| Need rack/update-domain resiliency | Availability set |
| Need autoscaling identical VMs | VM Scale Set |
| Need repeatable resource deployment | ARM/Bicep |
| Need private container image registry | ACR |
| Need simple one-off container | ACI |
| Need managed scalable container app | Container Apps |
| Need managed web hosting | App Service |
| Need App Service scale control | App Service plan |
| Need staging before production | Deployment slot |
| Need App Service outbound private access | VNet integration |
| Need private inbound App Service access | Private endpoint |
| Need App Service backup | App Service backup |

## Cleanup

Delete the resource group to avoid ongoing cost:

```bash
az group delete --name rg-az104-lab07-compute --yes --no-wait
```

## Final Mental Model

```text
Need OS control? VM.
Need repeatable deployment? ARM/Bicep.
Need more CPU/RAM? Resize VM.
Need more persistent storage? Attach data disk.
Need read-heavy disk performance? ReadOnly host caching.
Need host-level encryption? Encryption at host.
Need datacenter-level resiliency? Availability zone.
Need rack/update-domain resiliency? Availability set.
Need autoscaling identical VMs? VMSS.
Need private container registry? ACR.
Need quick simple container? ACI.
Need managed scalable container app? Container Apps.
Need managed web hosting? App Service.
Need scale App Service workers? App Service plan scale-out.
Need staging/test before production? Deployment slot.
Need friendly web name? Custom domain.
Need HTTPS? TLS certificate binding.
Need App Service outbound to VNet? VNet integration.
Need App Service private inbound? Private endpoint.
Need App Service backup? App Service backup.
```
