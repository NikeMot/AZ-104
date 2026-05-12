# Lab 05 — Guided Networking

**Certification:** Microsoft AZ-104: Azure Administrator Associate  
**Domain:** Implement and manage virtual networking  
**Lab type:** Guided practice  
**Status:** Completed

## Scenario

This lab implemented a portal-first Azure networking environment for a simulated operations workload. The design used a hub/workload VNet architecture with segmented subnets, secure administration, traffic filtering, routing, private PaaS connectivity patterns, DNS, load balancing, and troubleshooting.

## Architecture Summary

The lab used a hub/workload model:

```text
Internet
   |
   | HTTP/80
   v
Public IP
   |
Azure Load Balancer
   |
Backend web VMs without public IPs

Hub VNet: 10.60.0.0/16
├── snet-hub-mgmt
└── AzureBastionSubnet

Workload VNet: 10.70.0.0/16
├── snet-web
└── snet-data
```

## AZ-104 Objectives Covered

### Configure and manage virtual networks in Azure

- Created and configured virtual networks and subnets
- Created and configured virtual network peering
- Configured public IP addresses
- Configured user-defined routes
- Reviewed and practised network connectivity troubleshooting

### Configure secure access to virtual networks

- Created and configured NSGs and ASGs
- Reviewed effective security rules in NSGs
- Implemented or reviewed Azure Bastion
- Configured or reviewed service endpoints for Azure PaaS
- Configured or reviewed private endpoints for Azure PaaS

### Configure name resolution and load balancing

- Configured or reviewed private DNS
- Configured a public Azure Load Balancer
- Troubleshot load balancing patterns

## Implementation Summary

Key activities included:

- creating a dedicated networking resource group
- creating a hub VNet for management services
- creating a workload VNet for application resources
- creating web and data subnets
- configuring VNet peering between hub and workload VNets
- creating and associating NSGs to subnets
- creating an ASG for web servers
- allowing HTTP traffic while denying direct internet SSH
- creating backend web VMs without public IPs
- deploying or reviewing Azure Bastion for secure administration
- creating a public IP and public Load Balancer
- configuring backend pool, health probe, and load balancing rule
- creating a route table and user-defined route
- configuring or reviewing service endpoint access to Storage
- configuring or reviewing private endpoint access to Storage
- creating or reviewing private DNS zones and records
- reviewing effective security rules
- using Network Watcher tools conceptually for troubleshooting

## Why the Architecture Matters

The lab reinforced that Azure networking is not just resource creation. It is about controlling:

- which resources can communicate
- which path traffic takes
- which traffic is allowed or denied
- how administrators connect securely
- how PaaS services are accessed privately or from selected subnets
- how DNS supports private name resolution
- how traffic is distributed to healthy backend workloads

## Exam Patterns Reinforced

| Requirement pattern | Correct AZ-104 thinking |
|---|---|
| Private VNet-to-VNet communication | VNet peering |
| Secure VM access without public IPs | Azure Bastion |
| Allow or deny traffic by port/protocol/source | NSG |
| Group VM NICs for security rules | ASG |
| See actual NSG rules applied to NIC | Effective security rules |
| Check whether traffic is allowed or denied | IP flow verify |
| Force traffic through an appliance | User-defined route |
| Restrict public PaaS endpoint to subnet | Service endpoint and firewall rule |
| Give PaaS resource a private IP | Private endpoint |
| Resolve private names | Private DNS zone and VNet link |
| Distribute TCP/UDP traffic | Azure Load Balancer |
| Troubleshoot backend traffic failure | Check frontend, rule, probe, backend pool, VM service, and NSG |

## Key Lessons

- VNets define private network boundaries.
- Subnets provide segmentation for workloads and controls.
- VNet peering enables private communication between VNets.
- NSGs allow or deny traffic; they do not route traffic.
- UDRs control traffic path; they do not allow or deny traffic.
- Bastion reduces exposure by avoiding VM public IPs.
- Service endpoints and private endpoints solve different PaaS access problems.
- Load Balancer is Layer 4 and depends on frontend IP, backend pool, probe, rule, VM service, and NSG.
- Network Watcher tools are selected based on the troubleshooting question being asked.

## Evidence Method

No screenshots are stored in this repository. Evidence is recorded through written validation notes, network design notes, troubleshooting notes, error notes, and reflection files.
