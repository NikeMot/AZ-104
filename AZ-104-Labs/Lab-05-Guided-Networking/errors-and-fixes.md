# Lab 05 Errors and Fixes

| Issue | Root cause | Fix or action | AZ-104 exam lesson |
|---|---|---|---|
| Bastion subnet not accepted | Subnet name or size incorrect | Use the exact name `AzureBastionSubnet` and an appropriate prefix such as `/26` | Bastion has strict subnet requirements |
| Backend VM is exposed publicly | Public IP assigned during VM creation | Remove public IP or recreate VM without one | Backend VMs should often sit behind load balancing and use Bastion for admin access |
| Peering does not work | Reverse peering missing, address spaces overlap, or NSG blocks traffic | Check both directions, non-overlapping CIDRs, and NSG rules | Peering enables private routing but does not bypass security rules |
| HTTP traffic blocked | NSG rule missing or lower-priority deny overrides expected flow | Check inbound rules and effective security rules | NSG priority and effective rules matter |
| Load Balancer does not respond | Probe unhealthy, backend pool incomplete, web service stopped, or NSG blocks traffic | Check frontend, rule, probe, backend pool, VM service, and NSG | Load Balancer failures are usually chain failures |
| Private endpoint not resolving | Private DNS zone missing, not linked, or record absent | Check DNS zone, VNet link, and A record | Private endpoint design often depends on DNS |

## Notes

The main learning from this lab is that Azure networking issues are usually caused by one of four things: path, permission, DNS, or service health.
