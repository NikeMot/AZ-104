# Lab 06 Validation

## Resource Foundation

| Requirement | Status |
|---|---|
| Resource group created | Completed |
| Application VNet created | Completed |
| Shared-services VNet created | Completed |
| Address spaces confirmed as non-overlapping | Completed |
| Web subnet created | Completed |
| API subnet created | Completed |
| Private endpoint subnet created | Completed |
| AzureBastionSubnet created with exact required name | Completed |
| Shared-services subnet created | Completed |

## Connectivity Validation

| Requirement | Status |
|---|---|
| VNet peering configured from application VNet to shared-services VNet | Completed |
| VNet peering configured from shared-services VNet to application VNet | Completed |
| Peering status reviewed as connected | Completed |
| Private IP connectivity model understood | Completed |

## Security Validation

| Requirement | Status |
|---|---|
| Web subnet NSG created or designed | Completed |
| API subnet NSG created or designed | Completed |
| Web tier can receive intended frontend traffic | Completed |
| API tier is not directly internet-exposed | Completed |
| ASG pattern documented for web/API tier grouping | Completed |
| Backend VMs do not require public IP addresses | Completed |

## Bastion Validation

| Requirement | Status |
|---|---|
| Bastion subnet exists | Completed |
| Bastion public IP purpose understood | Completed |
| Bastion public IP separated from Load Balancer public IP | Completed |
| Admin access path documented | Completed |

## Load Balancer Validation

| Requirement | Status |
|---|---|
| Public Load Balancer pattern documented | Completed |
| Frontend public IP documented | Completed |
| Backend pool documented | Completed |
| Health probe documented | Completed |
| Load balancing rule documented | Completed |
| Load Balancer troubleshooting chain documented | Completed |

## Private Endpoint and DNS Validation

| Requirement | Status |
|---|---|
| Storage private endpoint pattern documented | Completed |
| Private endpoint subnet documented | Completed |
| Private DNS zone requirement documented | Completed |
| VNet link requirement documented | Completed |
| Service endpoint vs private endpoint comparison documented | Completed |

## Routing Validation

| Requirement | Status |
|---|---|
| Route table / UDR pattern documented | Completed |
| Forced egress path through virtual appliance understood | Completed |
| NSG vs UDR distinction documented | Completed |

## Network Watcher Validation

| Troubleshooting requirement | Correct tool | Status |
|---|---|---|
| Check NSG allow/deny | IP flow verify | Completed |
| Check route path | Next hop | Completed |
| Check effective NSG rules | Effective security rules | Completed |
| Check effective routes | Effective routes | Completed |
| Monitor ongoing connectivity | Connection Monitor | Completed |

## Completion Statement

Lab 06 is complete because the networking design can be explained from requirements and mapped to the correct Azure features without relying on a guided walkthrough.
