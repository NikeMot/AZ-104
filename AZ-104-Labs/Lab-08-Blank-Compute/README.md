# Lab 08 — Blank Compute Challenge

**Certification:** Microsoft AZ-104: Azure Administrator Associate  
**Domain:** Deploy and manage Azure compute resources  
**Lab type:** Blank from-scratch challenge  
**Status:** Completed  
**Difficulty:** Harder than exam

## Scenario Summary

This lab required designing an Azure compute architecture from requirements only. The goal was to prove that compute services could be selected correctly without a guided walkthrough.

The scenario involved four workload types:

```text
1. A legacy admin application requiring full OS control.
2. A public web app requiring platform-managed hosting.
3. A containerised microservice requiring managed scaling.
4. A fleet of similar web VMs requiring autoscale.
```

## Business Requirements

The design had to satisfy:

```text
1. Legacy workload must run on a VM.
2. VM must have persistent application data storage.
3. VM must support resizing.
4. VM disk performance/caching choices must be documented.
5. VM resiliency choice must be justified.
6. Similar web VMs must support autoscaling.
7. Container images must be stored privately in Azure.
8. A simple test container must run without Kubernetes.
9. A scalable container app must support ingress and scaling.
10. A managed web app must be hosted without managing the OS.
11. The web app must support staging before production.
12. The web app must support custom DNS and HTTPS.
13. The web app must have a backup strategy.
14. The web app must support private/outbound network integration.
15. Repeatable deployment must be considered using ARM/Bicep.
```

## Target Architecture

```text
Resource Group
   |
   +--> VNet / subnets
   |
   +--> VM for legacy workload
   |      ├── OS disk
   |      └── Data disk
   |
   +--> VM Scale Set for scalable VM workload
   |
   +--> Azure Container Registry
   |      ├── Azure Container Instance
   |      └── Azure Container App
   |
   +--> App Service Plan
          └── App Service Web App
              ├── staging slot
              ├── custom domain / TLS
              ├── networking
              └── backup
```

## Compute Feature Selection

| Requirement | Azure feature | Reason |
|---|---|---|
| Full OS control | Virtual Machine | VM gives operating system-level control. |
| Persistent application storage | Managed data disk | Data disk separates application data from the OS disk. |
| More CPU/RAM | VM resize | VM size controls CPU, memory, throughput, and cost. |
| Read-heavy disk workload | ReadOnly host caching | Improves read performance where appropriate. |
| Host-level encryption | Encryption at host | Encrypts VM data at the host layer. |
| Datacenter resiliency | Availability zone | Protects against zone/datacenter failure. |
| Similar autoscaling VMs | VM Scale Set | Provides fleet management and autoscale. |
| Private image storage | Azure Container Registry | Stores container images; does not run them. |
| Simple test container | Azure Container Instances | Runs a simple container quickly without orchestration. |
| Managed scalable container app | Azure Container Apps | Provides ingress, scaling, and revisions. |
| Managed web hosting | App Service | Hosts web apps without OS management. |
| App Service compute boundary | App Service plan | Controls worker tier, scaling, and features. |
| Staged deployment | Deployment slot | Allows staging, testing, and swap. |
| Friendly hostname | Custom domain | Maps a DNS name to the web app. |
| HTTPS | TLS certificate binding | Secures the custom hostname. |
| App outbound access to VNet | VNet integration | Allows App Service to reach private resources. |
| Private inbound access to App Service | Private endpoint | Provides private inbound access to the app. |
| Repeatable deployment | ARM/Bicep | Provides declarative, repeatable infrastructure deployment. |

## VM Design

The VM was selected for the legacy workload because the application required OS-level control.

The VM design included:

```text
VM resource
NIC
VNet/subnet placement
OS disk
managed data disk
size review
host caching decision
encryption at host decision
availability decision
```

Key lesson:

```text
VMs provide control, but also increase operational responsibility.
```

## VMSS Design

VM Scale Sets were selected for the group of similar web VMs because the requirement called for autoscaling identical instances.

The design included:

```text
initial instance count
autoscale profile
scale-out threshold
scale-in threshold
minimum/default/maximum instance limits
```

Key lesson:

```text
VMSS is not just availability. It is scalable fleet management for similar VM instances.
```

## Container Design

The container architecture used three separate concepts:

```text
ACR = stores private images
ACI = runs simple containers quickly
Container Apps = managed scalable app containers
```

Key trap:

```text
ACR does not run containers.
```

## App Service Design

The App Service architecture included:

```text
App Service plan
Web App
Scale up / scale out review
Deployment slot
Custom domain and TLS plan
VNet integration review
Private endpoint review
Backup plan
```

Key distinction:

```text
App Service plan = compute and scaling boundary
App Service app = the web application resource
```

## ARM/Bicep Note

ARM templates and Bicep were included as the repeatable deployment mechanism.

Key exam patterns:

```text
Repeatable deployment = ARM/Bicep
Preview changes = what-if
Environment-specific values = parameters
Dependencies = deployment order/resource relationship
```

## Objective Mapping

This lab covered:

- Interpret an ARM template or Bicep file
- Modify an ARM template or Bicep file
- Deploy resources by using ARM/Bicep
- Export deployment as ARM template or convert ARM to Bicep
- Create a virtual machine
- Configure encryption at host
- Move a VM to another resource group, subscription, or region
- Manage VM sizes
- Manage VM disks
- Deploy VMs to availability zones and availability sets
- Deploy and configure VM Scale Sets
- Create and manage Azure Container Registry
- Provision containers using Azure Container Instances
- Provision containers using Azure Container Apps
- Manage sizing and scaling for containers
- Provision an App Service plan
- Configure scaling for an App Service plan
- Create an App Service
- Configure certificates and TLS
- Map custom DNS names
- Configure backup
- Configure networking settings
- Configure deployment slots

## Exam Patterns Learned

| Exam wording | Correct thinking |
|---|---|
| Full OS control | VM |
| More VM CPU/RAM | Resize VM |
| Extra persistent VM storage | Managed data disk |
| Read-heavy disk performance | ReadOnly host caching |
| Datacenter-level resiliency | Availability zone |
| Rack/update-domain resiliency | Availability set |
| Autoscaling identical VM instances | VM Scale Set |
| Private container image storage | ACR |
| Quick simple container | ACI |
| Managed scalable HTTP container | Container Apps |
| Managed web hosting | App Service |
| App Service compute/scale | App Service plan |
| Staging before production | Deployment slot |
| Friendly web name | Custom domain |
| HTTPS | TLS binding |
| Outbound App Service to VNet | VNet integration |
| Private inbound to App Service | Private endpoint |
| Repeatable deployment | ARM/Bicep |

## Final Challenge Answer

```text
Full OS control: Virtual Machine
Autoscaling identical VMs: Virtual Machine Scale Set
Private image storage: Azure Container Registry
Quick test container: Azure Container Instances
Managed scalable HTTP container app: Azure Container Apps
Managed web app with staging: App Service + deployment slot
```
