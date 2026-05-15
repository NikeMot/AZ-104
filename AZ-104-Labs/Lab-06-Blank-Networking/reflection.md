# Lab 06 Reflection

## What this lab proved

This lab proved that the networking architecture from Lab 05 could be reproduced from requirements without hand-holding.

The main achievement was moving from:

```text
Following steps
```

to:

```text
Reading requirements -> choosing the correct Azure networking features -> justifying the design
```

That is the real AZ-104 skill.

## Key concepts reinforced

### NSG vs UDR

An NSG controls whether traffic is allowed or denied.

A UDR controls where traffic is sent.

```text
NSG = filtering
UDR = routing
```

An NSG cannot force traffic through a firewall. A UDR cannot allow traffic that an NSG denies.

### Service endpoint vs private endpoint

A service endpoint keeps the PaaS public endpoint model but allows selected subnet access through the PaaS firewall.

A private endpoint gives the PaaS service a private IP in the VNet.

```text
Service endpoint = subnet-restricted access to public PaaS endpoint
Private endpoint = private IP for PaaS
```

### Private DNS

Private endpoint access is incomplete without correct DNS.

```text
Private endpoint = private IP
Private DNS = normal name resolves to private IP
VNet link = which VNets can resolve it
```

### Bastion vs Load Balancer public IP

Bastion and Load Balancer both use public IPs, but they are not the same path.

```text
Bastion public IP = administrator access
Load Balancer public IP = user/application access
```

Bastion is not the web frontend.

### VNet peering

VNet peering connects non-overlapping VNets privately.

It does not automatically fix:

```text
NSG blocks
UDR mistakes
DNS resolution
application issues
```

## Most important exam patterns

| Requirement | Think |
|---|---|
| Private network boundary | VNet |
| Separate tiers | Subnets |
| Allow/deny traffic | NSG |
| Avoid hard-coded VM IPs in rules | ASG |
| Connect two VNets privately | VNet peering |
| Secure admin access without VM public IPs | Bastion |
| One public frontend for TCP traffic | Public Load Balancer |
| Private IP for PaaS | Private endpoint |
| Normal FQDN resolves privately | Private DNS |
| Force traffic through firewall/NVA | UDR |
| Check NSG allow/deny | IP flow verify |
| Check route path | Next hop |
| Monitor connectivity | Connection Monitor |

## What would change in production

In a more production-grade design, the hub VNet would likely contain:

```text
Azure Firewall
AzureBastionSubnet
GatewaySubnet for VPN/ExpressRoute
central DNS forwarding
central logging/security tooling
```

The application VNet would be a spoke containing:

```text
web subnet
API subnet
private endpoint subnet
application workload resources
```

This lab intentionally focused on AZ-104 feature selection rather than full enterprise landing zone complexity.

## Readiness judgement

This lab strengthens exam readiness because it tests feature selection under constraints:

```text
No public backend VM IPs -> Bastion
Private PaaS access -> private endpoint
Normal FQDN with private endpoint -> private DNS
Traffic through firewall -> UDR
Allow/deny traffic -> NSG
Single public TCP frontend -> Load Balancer
Troubleshooting path -> Network Watcher tools
```

The domain is ready when these decisions are automatic.
