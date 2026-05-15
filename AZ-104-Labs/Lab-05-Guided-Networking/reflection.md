# Lab 05 Reflection

## What this lab is really about

This lab is about understanding Azure networking as an architecture, not as a list of portal screens.

The architecture represents a secure application network:

```text
Public users enter through a Load Balancer.
Administrators enter through Bastion.
Application tiers are separated by subnets.
Traffic is filtered by NSGs.
Changing VM groups can be represented by ASGs.
Shared services live in a separate VNet.
VNet peering connects the application network to the shared network.
Storage can be accessed privately through a private endpoint and private DNS.
Routes can force traffic through a firewall or appliance path.
Network Watcher tools prove where traffic is allowed, blocked, or routed.
```

## Architecture I should remember

```text
vnet-app = application/spoke VNet
vnet-shared = hub-like/shared-services VNet

Bastion public IP = admin path
Load Balancer public IP = user/application path

Service endpoint = subnet-restricted access to public PaaS endpoint
Private endpoint = private IP for PaaS inside VNet
Private DNS = normal FQDN resolves to private endpoint IP
```

## Most important decisions

1. Use `vnet-app` for application workloads.
2. Use `vnet-shared` as the hub-like shared-services network.
3. Use subnets to separate web, API, private endpoint, and Bastion functions.
4. Use VNet peering for private communication between app and shared networks.
5. Use NSGs for allow/deny traffic filtering.
6. Use ASGs to avoid hard-coding VM private IP addresses in security rules.
7. Avoid public IPs on backend VMs.
8. Use Azure Bastion for admin access to private VMs.
9. Remember that Bastion has its own public IP and does not share the Load Balancer frontend public IP.
10. Use a public Load Balancer for user/application traffic into web VMs.
11. Use UDRs to control traffic path through a firewall/NVA.
12. Use service endpoints when the PaaS public endpoint remains but access is restricted to selected subnets.
13. Use private endpoints when the PaaS service needs a private IP in the VNet.
14. Use private DNS so applications can keep using normal service FQDNs.
15. Use Network Watcher tools based on the exact troubleshooting question.

## Exam patterns reinforced

| Exam wording | Correct response |
|---|---|
| Need private network boundary | VNet |
| Need to separate web/API/database tiers | Subnets |
| Need to allow or deny traffic | NSG |
| Need security rules for a changing set of VMs | ASG + NSG |
| Need private communication between non-overlapping VNets | VNet peering |
| Need secure RDP/SSH without VM public IPs | Azure Bastion |
| Need one public IP for TCP traffic to multiple VMs | Public Load Balancer |
| Need subnet access to Storage public endpoint | Service endpoint + storage firewall |
| Need Storage reachable by private IP | Private endpoint |
| Need normal FQDN to resolve to private IP | Private DNS zone + VNet link |
| Need to force outbound traffic through firewall | UDR |
| Need to test NSG allow/deny | IP flow verify |
| Need to check selected route | Next hop |
| Need to inspect all effective NSG rules | Effective security rules |
| Need to monitor connectivity over time | Connection Monitor |

## Key correction to my understanding

Bastion is not the same as the public frontend for the application.

```text
Azure Bastion public IP:
Admin browser -> Bastion -> VM private IP

Load Balancer public IP:
Internet user -> Load Balancer -> web VM/backend pool
```

They are separate resources with separate public IPs.

## What I should be able to explain now

- Why a VNet exists.
- Why subnets exist.
- Why the web, API, private endpoint, and Bastion subnets are separate.
- Why `AzureBastionSubnet` must be named exactly that.
- Why Bastion needs a public IP but VMs do not.
- Why Load Balancer and Bastion do not share the same public IP.
- Why service endpoints and private endpoints are not the same thing.
- Why private DNS is required for private endpoint FQDN resolution.
- Why NSGs and UDRs solve different problems.
- Why VNet peering does not override NSGs or route issues.
- Which Network Watcher tool answers which troubleshooting question.

## Review items

- Continue reviewing NSG vs UDR.
- Continue reviewing service endpoint vs private endpoint.
- Continue reviewing private endpoint DNS.
- Continue reviewing Bastion placement in hub/spoke architecture.
- Continue reviewing Load Balancer health probe and backend pool troubleshooting.
- Continue reviewing Network Watcher tool selection.

## Readiness judgement

This lab gives practical readiness for the AZ-104 virtual networking domain if the architecture can be explained from memory and the correct Azure feature can be selected from requirement wording.

The key readiness test is this:

```text
Can I look at a requirement and immediately decide whether it needs VNet, subnet, NSG, ASG, peering, Bastion, service endpoint, private endpoint, private DNS, UDR, Load Balancer, or Network Watcher?
```

If yes, this domain becomes much easier.
