# Lab 05 — Guided Networking Architecture Lab

**Certification:** Microsoft AZ-104: Azure Administrator Associate  
**Domain:** Implement and manage virtual networking  
**Lab type:** Guided practice / architecture-first implementation  
**Status:** Completed  
**Difficulty:** Harder-than-standard guided lab

## Purpose

This lab builds a small enterprise-style Azure network and explains the architecture behind it. The goal is not just to create networking resources. The goal is to understand how Azure networking controls communication, security, routing, private PaaS access, public frontend access, and troubleshooting.

The lab simulates a company hosting an application in Azure with:

- public user access to a web tier
- private backend/API segmentation
- secure administrator access without VM public IPs
- private access to Azure Storage through a private endpoint
- a shared-services VNet connected through peering
- route control through a user-defined route
- Layer 4 load balancing
- Network Watcher troubleshooting patterns

## Architecture Summary

The lab uses an application VNet and a shared-services VNet.

```text
Internet users
   |
   v
Public Load Balancer frontend public IP
   |
   v
snet-web in vnet-app
   |
   v
snet-api in vnet-app
   |
   v
Storage account through private endpoint + private DNS

Administrators
   |
   v
Azure Bastion public IP
   |
   v
Azure Bastion in AzureBastionSubnet
   |
   v
VM private IPs

vnet-app <---- VNet peering ----> vnet-shared
```

## Network Design

```text
Resource Group: rg-az104-lab05-networking

vnet-app: 10.50.0.0/16
├── snet-web: 10.50.1.0/24
├── snet-api: 10.50.2.0/24
├── snet-private-endpoints: 10.50.3.0/24
└── AzureBastionSubnet: 10.50.10.0/26

vnet-shared: 10.60.0.0/16
└── snet-shared: 10.60.1.0/24

Storage Account
└── Private endpoint for blob sub-resource in snet-private-endpoints
└── Private DNS integration for blob privatelink namespace

Public Load Balancer
├── Frontend public IP: pip-web-lb-lab05
├── Backend pool: be-web-vms
├── Health probe: hp-http
└── Load balancing rule: rule-http

Azure Bastion
├── Public IP: pip-bas-az104-lab05
└── Subnet: AzureBastionSubnet
```

## Hub/Spoke Clarification

In this lab, `vnet-shared` is the hub-like VNet and `vnet-app` is the spoke/application VNet.

This is a starter hub/spoke-style design rather than a full production hub-and-spoke network. In a larger production design, the hub VNet commonly contains Azure Firewall, VPN/ExpressRoute Gateway, DNS services, Bastion, and other shared services. The spoke VNets contain application workloads.

For learning purposes, this lab places Bastion in `vnet-app` so the Bastion pattern is easy to understand:

```text
Bastion public IP = admin access path
Load Balancer public IP = application/user traffic path
```

These are not the same public IP. Bastion is for administrators connecting to private VMs. The Load Balancer frontend public IP is for users reaching the web application.

## AZ-104 Objectives Covered

### Configure and manage virtual networks in Azure

- Create and configure virtual networks and subnets
- Create and configure virtual network peering
- Configure public IP addresses
- Configure user-defined routes
- Troubleshoot network connectivity

### Configure secure access to virtual networks

- Create and configure network security groups and application security groups
- Evaluate effective security rules in NSGs
- Implement Azure Bastion
- Configure service endpoints for Azure PaaS
- Configure private endpoints for Azure PaaS

### Configure name resolution and load balancing

- Configure Azure DNS / private DNS for private endpoint resolution
- Configure an internal or public Load Balancer
- Troubleshoot load balancing

## Core Architecture Decisions

| Design decision | Why it was used | AZ-104 pattern |
|---|---|---|
| VNet | Provides private network address space | Private Azure network boundary |
| Subnets | Segment web, API, private endpoint, and Bastion areas | Workload separation and control boundaries |
| NSGs | Allow or deny traffic by source, destination, protocol, and port | Traffic filtering |
| ASGs | Group changing VM NICs for NSG rules | Avoid hard-coded IP security rules |
| VNet peering | Connect vnet-app and vnet-shared privately | Private VNet-to-VNet communication |
| Bastion | Provide admin SSH/RDP without VM public IPs | Secure VM administration |
| Service endpoint | Allow selected subnet access to PaaS public endpoint | Subnet-restricted PaaS access |
| Private endpoint | Give PaaS service a private IP in the VNet | Private PaaS access |
| Private DNS | Resolve normal PaaS FQDN to private endpoint IP | Private endpoint name resolution |
| UDR | Force traffic through a firewall/NVA path | Route control |
| Public Load Balancer | Expose one public frontend and distribute TCP traffic | Layer 4 load balancing |
| Network Watcher | Diagnose routing, filtering, and connectivity | Troubleshooting evidence |

## Implementation Summary

Completed activities:

- Created `rg-az104-lab05-networking`
- Created `vnet-app` with segmented subnets
- Created `vnet-shared` with a shared-services subnet
- Configured VNet peering between `vnet-app` and `vnet-shared`
- Created NSGs for web and API subnet control
- Created ASGs for tier-based security rule design
- Reviewed Bastion placement and public IP purpose
- Configured or reviewed Azure Bastion for private VM administration
- Configured or reviewed service endpoint access to Storage
- Configured or reviewed private endpoint access to Storage
- Explained private DNS requirement for private endpoint FQDN resolution
- Created or reviewed route table / UDR forced-routing pattern
- Created or reviewed public Load Balancer components
- Reviewed Network Watcher tools for troubleshooting

## Portal-First Task List

### Task 1 — Resource group

Create `rg-az104-lab05-networking` in UK South.

### Task 2 — Application VNet

Create `vnet-app` with address space `10.50.0.0/16` and subnets:

- `snet-web` — `10.50.1.0/24`
- `snet-api` — `10.50.2.0/24`
- `snet-private-endpoints` — `10.50.3.0/24`
- `AzureBastionSubnet` — `10.50.10.0/26`

### Task 3 — Shared VNet and peering

Create `vnet-shared` with address space `10.60.0.0/16` and subnet `snet-shared` as `10.60.1.0/24`. Peer `vnet-app` and `vnet-shared` in both directions.

### Task 4 — NSGs

Create:

- `nsg-web`
- `nsg-api`

Associate `nsg-web` with `snet-web` and `nsg-api` with `snet-api`. Add an HTTP allow rule to `nsg-web` where required.

### Task 5 — ASGs

Create:

- `asg-web`
- `asg-api`

Use these to understand how NSG rules can target logical application groups rather than hard-coded IP addresses.

### Task 6 — Azure Bastion

Create or review Azure Bastion in `AzureBastionSubnet` with public IP `pip-bas-az104-lab05`. Understand that Bastion's public IP is for admin access only and is separate from the Load Balancer frontend public IP.

### Task 7 — Service endpoint

Enable `Microsoft.Storage` service endpoint on `snet-web` and understand the pattern of selected-subnet access to a storage account public endpoint.

### Task 8 — Private endpoint and private DNS

Create or review a blob private endpoint in `snet-private-endpoints`. Integrate with the correct private DNS zone so the standard storage FQDN resolves to the private endpoint IP.

### Task 9 — Route table / UDR

Create `rt-web-forced-egress` and a default route to a virtual appliance IP such as `10.60.1.4` to simulate forced egress through a firewall or NVA.

### Task 10 — Public Load Balancer

Create or review:

- frontend public IP
- backend pool
- health probe
- load balancing rule

Use this to understand Layer 4 distribution to healthy backend VMs.

### Task 11 — Network Watcher troubleshooting

Review tool selection:

| Question | Tool |
|---|---|
| Is this flow allowed or denied by NSG? | IP flow verify |
| What NSG rules apply to this NIC? | Effective security rules |
| Which route is selected? | Next hop |
| Which routes apply to this NIC? | Effective routes |
| Is connectivity stable over time? | Connection Monitor |

## Azure CLI Reference

```bash
az group create --name rg-az104-lab05-networking --location uksouth
```

```bash
az network vnet create \
  --resource-group rg-az104-lab05-networking \
  --name vnet-app \
  --address-prefix 10.50.0.0/16 \
  --subnet-name snet-web \
  --subnet-prefix 10.50.1.0/24
```

```bash
az network vnet subnet create --resource-group rg-az104-lab05-networking --vnet-name vnet-app --name snet-api --address-prefixes 10.50.2.0/24
az network vnet subnet create --resource-group rg-az104-lab05-networking --vnet-name vnet-app --name snet-private-endpoints --address-prefixes 10.50.3.0/24
az network vnet subnet create --resource-group rg-az104-lab05-networking --vnet-name vnet-app --name AzureBastionSubnet --address-prefixes 10.50.10.0/26
```

```bash
az network vnet create \
  --resource-group rg-az104-lab05-networking \
  --name vnet-shared \
  --address-prefix 10.60.0.0/16 \
  --subnet-name snet-shared \
  --subnet-prefix 10.60.1.0/24
```

```bash
az network vnet peering create --resource-group rg-az104-lab05-networking --name peer-app-to-shared --vnet-name vnet-app --remote-vnet vnet-shared --allow-vnet-access
az network vnet peering create --resource-group rg-az104-lab05-networking --name peer-shared-to-app --vnet-name vnet-shared --remote-vnet vnet-app --allow-vnet-access
```

```bash
az network nsg create --resource-group rg-az104-lab05-networking --name nsg-web
az network nsg create --resource-group rg-az104-lab05-networking --name nsg-api
```

```bash
az network nsg rule create \
  --resource-group rg-az104-lab05-networking \
  --nsg-name nsg-web \
  --name Allow-HTTP-Inbound \
  --priority 100 \
  --direction Inbound \
  --access Allow \
  --protocol Tcp \
  --source-address-prefixes Internet \
  --source-port-ranges "*" \
  --destination-address-prefixes "*" \
  --destination-port-ranges 80
```

```bash
az network vnet subnet update --resource-group rg-az104-lab05-networking --vnet-name vnet-app --name snet-web --network-security-group nsg-web
az network vnet subnet update --resource-group rg-az104-lab05-networking --vnet-name vnet-app --name snet-api --network-security-group nsg-api
```

```bash
az network asg create --resource-group rg-az104-lab05-networking --name asg-web --location uksouth
az network asg create --resource-group rg-az104-lab05-networking --name asg-api --location uksouth
```

```bash
az network public-ip create --resource-group rg-az104-lab05-networking --name pip-bas-az104-lab05 --sku Standard --location uksouth
az network bastion create --resource-group rg-az104-lab05-networking --name bas-az104-lab05 --public-ip-address pip-bas-az104-lab05 --vnet-name vnet-app --location uksouth
```

```bash
az network vnet subnet update --resource-group rg-az104-lab05-networking --vnet-name vnet-app --name snet-web --service-endpoints Microsoft.Storage
```

```bash
az network route-table create --resource-group rg-az104-lab05-networking --name rt-web-forced-egress --location uksouth
az network route-table route create --resource-group rg-az104-lab05-networking --route-table-name rt-web-forced-egress --name default-to-firewall --address-prefix 0.0.0.0/0 --next-hop-type VirtualAppliance --next-hop-ip-address 10.60.1.4
az network vnet subnet update --resource-group rg-az104-lab05-networking --vnet-name vnet-app --name snet-web --route-table rt-web-forced-egress
```

```bash
az network public-ip create --resource-group rg-az104-lab05-networking --name pip-web-lb-lab05 --sku Standard --allocation-method Static
az network lb create --resource-group rg-az104-lab05-networking --name lb-web-public-lab05 --sku Standard --public-ip-address pip-web-lb-lab05 --frontend-ip-name fe-web-public --backend-pool-name be-web-vms
az network lb probe create --resource-group rg-az104-lab05-networking --lb-name lb-web-public-lab05 --name hp-http --protocol Tcp --port 80
az network lb rule create --resource-group rg-az104-lab05-networking --lb-name lb-web-public-lab05 --name rule-http --protocol Tcp --frontend-port 80 --backend-port 80 --frontend-ip-name fe-web-public --backend-pool-name be-web-vms --probe-name hp-http
```

## Exam Patterns Reinforced

| Requirement pattern | Correct thinking |
|---|---|
| Need private address space | VNet |
| Need workload segmentation | Subnets |
| Need traffic allow/deny | NSG |
| Need dynamic VM grouping in NSG rules | ASG |
| Need private VNet-to-VNet connectivity | VNet peering |
| Need secure RDP/SSH without VM public IPs | Azure Bastion |
| Need selected subnet access to PaaS public endpoint | Service endpoint + PaaS firewall |
| Need private IP for PaaS | Private endpoint |
| Need private endpoint to work using normal FQDN | Private DNS zone + VNet link |
| Need force traffic through appliance | UDR with next hop Virtual appliance |
| Need public Layer 4 distribution | Public Load Balancer |
| Need private Layer 4 distribution | Internal Load Balancer |
| Need NSG allow/deny check | IP flow verify |
| Need route path check | Next hop |
| Need combined NSG view | Effective security rules |
| Need full route table view | Effective routes |
| Need ongoing connectivity test | Connection Monitor |

## Retention Questions

1. You need to segment web and database VMs in the same VNet and apply different NSG rules. What should you create?  
   **Answer:** Separate subnets.

2. Two Azure VNets need private connectivity and their address spaces do not overlap. What should you configure?  
   **Answer:** VNet peering.

3. A PaaS service must be reachable using a private IP address from your VNet. What should you use?  
   **Answer:** Private endpoint.

4. A private endpoint exists, but clients still resolve the PaaS FQDN to a public IP. What is likely missing?  
   **Answer:** Private DNS zone integration or VNet link.

5. You need to force subnet traffic through a firewall. What should you configure?  
   **Answer:** UDR with next hop Virtual appliance.

6. You need to check whether TCP 443 from VM1 to VM2 is allowed by NSGs. What tool should you use?  
   **Answer:** IP flow verify.

7. You need to check which route Azure uses from a VM to a destination IP. What tool should you use?  
   **Answer:** Network Watcher Next hop.

8. Admins need browser-based SSH/RDP to private VMs without public IPs. What should you deploy?  
   **Answer:** Azure Bastion.

## Completion Criteria

The lab is complete when the following can be explained without notes:

- why `vnet-app` and `vnet-shared` exist
- why subnets are separated by function
- why Bastion uses its own public IP and does not share the Load Balancer frontend IP
- how service endpoints differ from private endpoints
- why private endpoint DNS matters
- how NSGs and UDRs solve different problems
- how Load Balancer frontend, backend pool, probe, and rule work together
- which Network Watcher tool answers each troubleshooting question

## Cleanup

Delete the resource group to remove lab resources and avoid ongoing charges:

```bash
az group delete --name rg-az104-lab05-networking --yes --no-wait
```

## Final Mental Model

```text
Need private network boundary? VNet.
Need segmentation? Subnet.
Need allow/deny? NSG.
Need dynamic VM grouping in NSG? ASG.
Need private VNet-to-VNet connection? Peering.
Need force next hop? UDR.
Need secure RDP/SSH without public IP? Bastion.
Need subnet access to PaaS public endpoint? Service endpoint.
Need private IP for PaaS? Private endpoint.
Need private endpoint to work by name? Private DNS.
Need public Layer 4 distribution? Public Load Balancer.
Need NSG flow check? IP flow verify.
Need route path check? Next hop.
Need combined NSG rules? Effective security rules.
Need all NIC routes? Effective routes.
Need continuous connectivity monitoring? Connection Monitor.
```
