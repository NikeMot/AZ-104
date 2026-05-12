# Lab 05 Reflection

## What this lab reinforced

This lab reinforced Azure networking architecture and troubleshooting through a portal-first implementation.

The key theme was understanding traffic flow:

```text
Who is trying to connect?
Where are they connecting from?
Where is the destination?
Which route is used?
Which security rule applies?
Does DNS resolve correctly?
Is the target service healthy?
```

## Most important decisions

1. Use a hub VNet for shared management services.
2. Use a workload VNet for application resources.
3. Use subnets to segment web and data/private endpoint resources.
4. Use VNet peering for private connectivity between VNets.
5. Use NSGs to allow or deny traffic.
6. Use ASGs to group VM NICs for NSG rules.
7. Avoid public IPs on backend VMs.
8. Use Azure Bastion for secure administration.
9. Use a Load Balancer for Layer 4 traffic distribution.
10. Use UDRs to control traffic path.
11. Use service endpoints to restrict public PaaS endpoints to selected subnets.
12. Use private endpoints to provide private IP access to PaaS services.
13. Use private DNS for private name resolution.
14. Use Network Watcher tools for connectivity troubleshooting.

## Exam patterns reinforced

- VNet peering is for private VNet-to-VNet communication.
- NSGs control allow/deny decisions.
- UDRs control next-hop routing.
- Bastion removes the need for public VM IPs.
- Load Balancer is Layer 4 and depends on frontend IP, rule, probe, backend pool, VM service, and NSG.
- Service endpoints and private endpoints solve different PaaS access problems.
- Effective security rules show the final NSG result.
- IP flow verify checks whether traffic is allowed or denied.
- Connection Monitor is for ongoing connectivity tests.

## Review items

- Continue reviewing NSG vs UDR.
- Continue reviewing service endpoint vs private endpoint.
- Continue reviewing Bastion requirements.
- Continue reviewing Load Balancer troubleshooting order.
- Continue reviewing Network Watcher tool selection.

## Readiness judgement

This lab provides practical readiness for the AZ-104 virtual networking domain when the architecture, routing, security, PaaS access, DNS, and troubleshooting patterns can be explained without notes.
