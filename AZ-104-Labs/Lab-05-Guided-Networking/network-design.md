# Lab 05 Network Design

## Architecture Summary

This lab used a hub/workload VNet design.

The hub VNet contains shared management services. The workload VNet contains application resources.

## Address Spaces

| Network | CIDR |
|---|---|
| Hub VNet | `10.60.0.0/16` |
| Workload VNet | `10.70.0.0/16` |

## Subnets

| Subnet | CIDR | Purpose |
|---|---|---|
| `snet-hub-mgmt` | `10.60.1.0/24` | Management subnet |
| `AzureBastionSubnet` | `10.60.2.0/26` | Required subnet for Azure Bastion |
| `snet-web` | `10.70.1.0/24` | Web workload subnet |
| `snet-data` | `10.70.2.0/24` | Data/private endpoint subnet |

## Security Controls

| Control | Purpose |
|---|---|
| NSG | Allows or denies traffic based on port, protocol, direction, source, and destination |
| ASG | Groups VM network interfaces logically for NSG rules |
| Azure Bastion | Provides secure VM access without VM public IP addresses |
| Service endpoint | Restricts PaaS public endpoint access to selected subnets |
| Private endpoint | Gives a PaaS resource a private IP address in the VNet |
| UDR | Overrides default routing behaviour and controls next hop path |

## Traffic Flow

### Admin access

Administrators should connect through Azure Bastion rather than exposing SSH/RDP directly to the internet.

### Web traffic

Internet traffic reaches the public Load Balancer frontend IP. The Load Balancer distributes TCP port 80 traffic to backend web VMs in the web subnet.

### Storage access

Service endpoint access restricts the public Storage endpoint to selected subnets. Private endpoint access provides private IP-based access to the Storage service.

### Peered VNet traffic

The hub and workload VNets communicate through VNet peering over Microsoft’s private backbone.

## Design Rationale

The design separates management, web, and data/private endpoint concerns. This supports clearer traffic control, better security boundaries, and easier troubleshooting.
