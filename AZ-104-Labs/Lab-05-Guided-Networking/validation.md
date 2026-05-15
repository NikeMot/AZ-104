# Lab 05 Validation

## Resource Foundation

| Requirement | Expected value | Status |
|---|---|---|
| Dedicated resource group created | `rg-az104-lab05-networking` | Completed |
| Application VNet created | `vnet-app` / `10.50.0.0/16` | Completed |
| Shared-services VNet created | `vnet-shared` / `10.60.0.0/16` | Completed |
| Web subnet created | `snet-web` / `10.50.1.0/24` | Completed |
| API subnet created | `snet-api` / `10.50.2.0/24` | Completed |
| Private endpoint subnet created | `snet-private-endpoints` / `10.50.3.0/24` | Completed |
| Bastion subnet created with exact required name | `AzureBastionSubnet` / `10.50.10.0/26` | Completed |
| Shared subnet created | `snet-shared` / `10.60.1.0/24` | Completed |

## Connectivity

| Requirement | Validation method | Status |
|---|---|---|
| VNet peering from app to shared configured | Check `peer-app-to-shared` state | Completed |
| VNet peering from shared to app configured | Check `peer-shared-to-app` state | Completed |
| Peering state reviewed | Confirm `Connected` | Completed |
| Address spaces confirmed as non-overlapping | `10.50.0.0/16` and `10.60.0.0/16` | Completed |

## Security Filtering

| Requirement | Expected value | Status |
|---|---|---|
| Web NSG created | `nsg-web` | Completed |
| API NSG created | `nsg-api` | Completed |
| Web NSG associated correctly | `snet-web` | Completed |
| API NSG associated correctly | `snet-api` | Completed |
| HTTP allow rule configured or reviewed | TCP/80 to web tier | Completed |
| ASG for web tier created | `asg-web` | Completed |
| ASG for API tier created | `asg-api` | Completed |
| NSG vs ASG relationship understood | ASG is referenced inside NSG rules | Completed |

## Secure Administration

| Requirement | Expected architecture | Status |
|---|---|---|
| Azure Bastion subnet exists | `AzureBastionSubnet` | Completed |
| Bastion public IP understood | `pip-bas-az104-lab05` | Completed |
| Bastion purpose understood | Admin SSH/RDP to private VMs | Completed |
| Bastion public IP separated from application frontend | Bastion IP is not Load Balancer IP | Completed |
| VM public IP avoidance pattern understood | Admin path uses Bastion | Completed |

## PaaS Access

| Requirement | Expected pattern | Status |
|---|---|---|
| Service endpoint pattern reviewed | `Microsoft.Storage` on `snet-web` | Completed |
| Storage firewall selected-network pattern understood | Allow selected subnet/IP range | Completed |
| Private endpoint pattern reviewed | Private IP in `snet-private-endpoints` | Completed |
| Private endpoint private IP concept understood | PaaS reachable through VNet IP | Completed |
| Private DNS requirement understood | Standard FQDN resolves to private IP | Completed |
| Service endpoint vs private endpoint distinction understood | Public endpoint restriction vs private IP | Completed |

## Routing

| Requirement | Expected value | Status |
|---|---|---|
| Route table created or reviewed | `rt-web-forced-egress` | Completed |
| UDR created or reviewed | `0.0.0.0/0` to virtual appliance | Completed |
| Simulated firewall/NVA IP documented | `10.60.1.4` | Completed |
| Route table associated to intended subnet | `snet-web` | Completed |
| NSG vs UDR distinction understood | NSG filters; UDR routes | Completed |

## Load Balancing

| Requirement | Expected value | Status |
|---|---|---|
| Public IP for Load Balancer created or reviewed | `pip-web-lb-lab05` | Completed |
| Load Balancer created or reviewed | `lb-web-public-lab05` | Completed |
| Frontend IP configured | `fe-web-public` | Completed |
| Backend pool configured | `be-web-vms` | Completed |
| Health probe configured | `hp-http` / TCP 80 | Completed |
| Load balancing rule configured | `rule-http` / TCP 80 | Completed |
| Bastion IP and Load Balancer IP distinction understood | Admin path vs user path | Completed |

## Troubleshooting Validation

| Troubleshooting question | Correct tool | Status |
|---|---|---|
| Is a packet allowed or denied by NSG? | IP flow verify | Completed |
| What NSG rules apply to a NIC? | Effective security rules | Completed |
| Which route is selected? | Next hop | Completed |
| Which routes apply to a NIC? | Effective routes | Completed |
| Is connectivity stable over time? | Connection Monitor | Completed |
| Is a backend receiving load-balanced traffic? | Probe, backend pool, rule, VM service, NSG | Completed |

## Exam-Readiness Validation

The lab is considered exam-ready when these statements can be explained without notes:

- A VNet provides private address space.
- Subnets segment workloads.
- NSGs allow or deny traffic.
- ASGs help avoid hard-coded IPs in NSG rules.
- VNet peering connects non-overlapping VNets privately.
- Bastion is for admin RDP/SSH and has its own public IP.
- The Load Balancer frontend public IP is for user/application traffic.
- Service endpoints restrict access to selected subnets while keeping the PaaS public endpoint model.
- Private endpoints give PaaS services private IPs in a VNet.
- Private DNS makes private endpoints work with normal FQDNs.
- UDRs control next-hop routing.
- Network Watcher tools must be selected based on the layer being tested.

## Completion Statement

This lab validates the main AZ-104 virtual networking architecture and troubleshooting patterns: VNets, subnets, VNet peering, NSGs, ASGs, Azure Bastion, service endpoints, private endpoints, private DNS, UDRs, public Load Balancer, and Network Watcher troubleshooting tools.
