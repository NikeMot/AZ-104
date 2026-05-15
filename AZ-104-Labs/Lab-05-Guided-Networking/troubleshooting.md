# Lab 05 Troubleshooting Notes

## Troubleshooting Principle

This lab reinforces one core rule:

```text
Do not guess. Identify the layer that is failing.
```

Azure networking troubleshooting should separate:

1. name resolution
2. topology and peering
3. routing
4. filtering
5. service health
6. load balancer health
7. guest OS/application behavior

## Architecture Being Troubleshot

```text
Internet users
   |
   v
Public Load Balancer frontend IP: pip-web-lb-lab05
   |
   v
snet-web in vnet-app
   |
   v
snet-api in vnet-app
   |
   v
Storage through private endpoint and private DNS

Administrators
   |
   v
Azure Bastion public IP: pip-bas-az104-lab05
   |
   v
Azure Bastion in AzureBastionSubnet
   |
   v
VM private IPs

vnet-app <----peering----> vnet-shared
```

## Network Watcher Tool Selection

| Problem | Correct tool | Why |
|---|---|---|
| Check whether a specific flow is allowed or denied by NSG | IP flow verify | Tests source/destination/protocol/port against effective NSG rules |
| See final NSG rules applied to a NIC | Effective security rules | Shows combined subnet and NIC NSG effects |
| Identify the next hop for traffic | Next hop | Shows the selected route and next-hop type |
| See all routes applying to a NIC | Effective routes | Shows system routes, UDRs, and propagated routes |
| Monitor connectivity over time | Connection Monitor | Tracks reachability and latency continuously |
| Capture packet-level evidence | Packet capture | Useful for deeper inspection after simpler checks |

## Load Balancer Troubleshooting Chain

When backend VMs do not receive load-balanced traffic, check the chain in this order:

```text
Frontend IP
   -> Load balancing rule
   -> Health probe
   -> Backend pool membership
   -> VM service listening on backend port
   -> NSG rules
   -> Guest OS firewall
```

## Private Endpoint Troubleshooting Chain

When private endpoint access fails, check in this order:

```text
Private DNS resolution
   -> Private endpoint connection status
   -> VNet link to private DNS zone
   -> Route path to private endpoint IP
   -> NSG rules if applicable
   -> PaaS firewall/public network setting
```

Key lesson:

```text
Private endpoint without correct private DNS commonly fails by FQDN.
```

## Bastion Troubleshooting Chain

When Bastion access fails, check:

```text
AzureBastionSubnet exists with exact name
Bastion deployment succeeded
Bastion has its own public IP
Target VM has private IP connectivity from Bastion VNet
NSG does not block required private RDP/SSH path
User has appropriate VM login/credential access
```

Important distinction:

```text
Bastion public IP = administrator access
Load Balancer public IP = application/user access
```

They are separate public IPs and should not be confused.

## Common Issues

| Issue | Likely cause | Fix/check | Exam lesson |
|---|---|---|---|
| Peered VNets cannot communicate | Peering missing, disconnected, address overlap, NSG block, route issue | Check address spaces, peering state, effective routes, NSGs | Peering enables private connectivity but does not bypass NSGs/routes |
| VM cannot be administered | VM has no public IP and Bastion is missing or broken | Check Bastion deployment and AzureBastionSubnet | Secure admin access should use Bastion, not public VM IPs |
| HTTP to web tier fails | NSG blocks port 80, LB rule/probe wrong, backend service not listening | Check NSG, LB probe, backend pool, VM service | Load balancing requires healthy backend service and allowed path |
| API subnet reachable from wrong source | NSG rule too broad | Narrow source to subnet/ASG as appropriate | NSGs should enforce least-permitted traffic |
| UDR appears not to work | Route table not associated, prefix mismatch, more specific route wins | Check effective routes/Next hop | UDR controls path, not allow/deny |
| Private endpoint exists but FQDN resolves public IP | Private DNS zone missing or not linked | Check private DNS zone, VNet link, A record | Private endpoint requires DNS for normal FQDN use |
| Storage access via service endpoint fails | Service endpoint not enabled or storage firewall lacks VNet rule | Check subnet service endpoint and storage networking | Service endpoint is subnet-restricted public endpoint access |
| Traffic blocked but route looks correct | NSG or guest firewall denying | Use IP flow verify/effective security rules | Routing and filtering are separate decisions |

## NSG vs UDR Decision Table

| Requirement | Use |
|---|---|
| Allow HTTP from Internet to web subnet | NSG |
| Deny SSH/RDP from Internet | NSG |
| Force outbound traffic through firewall/NVA | UDR |
| Determine whether traffic is allowed | IP flow verify |
| Determine where traffic is going | Next hop |

## Service Endpoint vs Private Endpoint Decision Table

| Requirement | Correct feature |
|---|---|
| Allow selected subnet to access Storage public endpoint | Service endpoint + storage firewall |
| Give Storage a private IP in the VNet | Private endpoint |
| Disable public network access to PaaS | Private endpoint pattern |
| Keep normal FQDN but resolve privately | Private DNS zone linked to VNet |

## Key Exam Patterns

- NSG = allow/deny traffic.
- UDR = control route path.
- Bastion = secure VM admin access without public VM IPs.
- Bastion public IP is separate from Load Balancer frontend public IP.
- Service endpoint = selected-subnet access to a PaaS public endpoint.
- Private endpoint = private IP for a PaaS resource.
- Private DNS = private endpoint works by normal FQDN.
- Effective security rules = final NSG view.
- IP flow verify = specific flow allowed/denied check.
- Next hop = route decision check.
- Connection Monitor = ongoing connectivity monitoring.
- Load Balancer troubleshooting starts with frontend, rule, probe, backend pool, service, and NSG.
