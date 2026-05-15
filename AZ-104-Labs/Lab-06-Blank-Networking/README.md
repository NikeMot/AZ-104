# Lab 06 — Blank Networking Challenge

**Certification:** Microsoft AZ-104: Azure Administrator Associate  
**Domain:** Implement and manage virtual networking  
**Lab type:** Blank from-scratch challenge  
**Status:** Completed  
**Difficulty:** Harder than exam

## Scenario Summary

This lab required designing and building an Azure networking architecture from requirements only. The goal was to prove understanding of Azure networking patterns without following a guided walkthrough.

The environment represented a small production web application with:

- public web access through a single frontend
- private backend/API tier
- secure administrator access without public VM IP addresses
- private storage access
- private DNS for private endpoint resolution
- a shared-services VNet connected to the application network
- route control for forced egress
- Azure-native troubleshooting using Network Watcher

## Business Requirements

The design had to satisfy these requirements:

```text
1. Web users must access the application through one public IP.
2. Backend VMs must not have public IP addresses.
3. Administrators must be able to connect securely to private VMs.
4. Web and API tiers must be separated.
5. API tier must not be directly exposed to the internet.
6. Storage must be reachable privately from the application network.
7. DNS must support private endpoint access using normal Azure service FQDNs.
8. The application network must connect privately to a shared-services network.
9. Outbound traffic from the web subnet must be capable of being routed through a firewall/NVA path.
10. Routing and NSG filtering must be troubleshootable using Azure-native tools.
```

## Target Architecture

```text
Internet users
   |
   v
Public Load Balancer
   |
   v
Web subnet
   |
   v
API subnet
   |
   v
Private endpoint to Storage

Administrators
   |
   v
Azure Bastion
   |
   v
Private VM access

Application VNet <---- VNet peering ----> Shared-services VNet
```

## Addressing Design

| Network area | Purpose | Address space / subnet |
|---|---|---|
| Application VNet | Main workload network | 10.80.0.0/16 |
| Web subnet | Public-facing web tier backend | Chosen from 10.80.0.0/16 |
| API subnet | Private backend/API tier | Chosen from 10.80.0.0/16 |
| Private endpoint subnet | Private endpoints for PaaS services | Chosen from 10.80.0.0/16 |
| AzureBastionSubnet | Azure Bastion deployment subnet | Chosen from 10.80.0.0/16, named exactly `AzureBastionSubnet` |
| Shared-services VNet | Hub-like network for shared services | 10.90.0.0/16 |
| Shared subnet | Firewall/NVA/shared services location | Chosen from 10.90.0.0/16 |

## Architecture Decisions

| Requirement | Azure feature used | Reason |
|---|---|---|
| Separate application tiers | Subnets | Subnets create network segmentation boundaries inside a VNet. |
| Allow/deny traffic | NSGs | NSGs filter traffic by source, destination, port, and protocol. |
| Avoid hard-coded IPs in rules | ASGs | ASGs allow logical VM grouping for NSG rules. |
| Connect app and shared networks | VNet peering | Peering provides private connectivity between non-overlapping VNets. |
| Secure VM administration | Azure Bastion | Bastion allows portal-based SSH/RDP without VM public IPs. |
| Public frontend for app traffic | Public Load Balancer | Load Balancer provides one public frontend IP and Layer 4 distribution. |
| Private PaaS access | Private endpoint | Private endpoint gives the PaaS resource a private IP in the VNet. |
| Private endpoint name resolution | Private DNS zone + VNet link | Private DNS makes the normal service FQDN resolve to the private endpoint IP. |
| Forced egress path | Route table / UDR | UDR controls next hop and can send traffic to firewall/NVA. |
| Route troubleshooting | Network Watcher Next hop / effective routes | These tools show route decisions. |
| Filtering troubleshooting | IP flow verify / effective security rules | These tools show NSG allow/deny results. |

## Security Design

Security principles applied:

- No backend VM public IPs.
- Web and API tiers are separated.
- API tier is not internet-facing.
- Bastion is used for administrator access.
- Bastion public IP is separate from application frontend public IP.
- NSGs are used for traffic filtering.
- ASGs are used where dynamic VM grouping is useful.
- Private endpoint is used for private Storage access.
- Private DNS is used to avoid public endpoint resolution.

## Routing Design

The forced egress pattern was based on:

```text
Web subnet -> Route table -> 0.0.0.0/0 -> Virtual appliance/firewall path
```

Key design principle:

```text
UDRs control where traffic goes.
NSGs control whether traffic is allowed.
```

A UDR cannot allow traffic that an NSG denies, and an NSG cannot force traffic through a firewall.

## Private Endpoint and DNS Design

Private endpoint design:

```text
Application VM
   |
   | normal Storage FQDN
   v
Private DNS zone linked to application VNet
   |
   | resolves to private endpoint IP
   v
Private endpoint subnet
   |
   v
Storage account
```

Key lesson:

```text
Private endpoint gives the private IP.
Private DNS makes the normal service name resolve to that private IP.
VNet link decides which VNets can resolve the private record.
```

## Load Balancer Design

The public web entry point used the Azure Load Balancer pattern:

```text
Frontend public IP
   -> Load balancing rule
   -> Health probe
   -> Backend pool
   -> Web VMs
```

This is a Layer 4 design for TCP/UDP traffic. It is not the same as Application Gateway, which is Layer 7 and handles HTTP-aware routing and WAF scenarios.

## Bastion Design

Bastion provides administrator access:

```text
Admin browser
   -> Bastion public IP
   -> Azure Bastion
   -> VM private IP
```

The Bastion public IP is not the same as the Load Balancer frontend public IP.

```text
Bastion public IP = admin path
Load Balancer public IP = user/application path
```

## Objective Mapping

This lab covered:

- Create and configure virtual networks and subnets
- Create and configure virtual network peering
- Configure public IP addresses
- Configure user-defined routes
- Troubleshoot network connectivity
- Create and configure NSGs and ASGs
- Evaluate effective security rules in NSGs
- Implement Azure Bastion
- Configure service endpoints for Azure PaaS
- Configure private endpoints for Azure PaaS
- Configure Azure DNS / Private DNS
- Configure a public Load Balancer
- Troubleshoot load balancing

## Exam Patterns Learned

| Exam wording | Correct thinking |
|---|---|
| Need private network boundary | VNet |
| Need segmentation | Subnets |
| Need traffic allow/deny | NSG |
| Need dynamic VM grouping in NSG rules | ASG |
| Need private communication between VNets | VNet peering |
| Need secure RDP/SSH without VM public IPs | Azure Bastion |
| Need selected subnet access to public PaaS endpoint | Service endpoint + firewall rule |
| Need private IP for PaaS | Private endpoint |
| Need private endpoint to work by FQDN | Private DNS zone + VNet link |
| Need traffic to go through firewall/NVA | UDR |
| Need one public frontend for TCP traffic | Public Load Balancer |
| Need route path check | Network Watcher Next hop |
| Need NSG allow/deny check | IP flow verify |
