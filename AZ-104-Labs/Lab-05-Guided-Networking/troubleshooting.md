# Lab 05 Troubleshooting Notes

## Network Watcher Tool Selection

| Problem | Correct tool |
|---|---|
| Check whether an NSG allows or denies traffic | IP flow verify |
| See final NSG rules applied to a NIC | Effective security rules |
| Identify the next hop for traffic | Next hop |
| Monitor connectivity over time | Connection Monitor |
| Capture packets for deep inspection | Packet capture |

## Load Balancer Troubleshooting Chain

When backend VMs do not receive load-balanced traffic, check the chain in this order:

```text
Frontend IP -> Load balancing rule -> Health probe -> Backend pool -> VM service -> NSG
```

## Common Issues

| Issue | Likely cause | Fix/check | Exam lesson |
|---|---|---|---|
| VM cannot be reached | VM has no public IP and Bastion is not configured | Use Azure Bastion or validate Bastion deployment | Secure VM access should not require public IPs |
| Peered VNets cannot communicate | Peering missing in one direction or NSG blocks traffic | Check both peerings and NSG rules | VNet peering enables private connectivity but does not override NSGs |
| HTTP to VM fails | NSG blocks port 80 or service not running | Check NSG and NGINX/web service | Traffic requires both allowed path and listening service |
| Load Balancer probe unhealthy | Backend service not listening or NSG blocks probe | Check health probe, backend port, service, and NSG | Load Balancer depends on healthy probes |
| UDR appears not to work | Route table not associated or destination prefix mismatch | Check subnet association and route prefix | UDR controls path, not allow/deny |
| Private endpoint DNS fails | Private DNS zone not linked or record missing | Check VNet link and A record | Private endpoint access often depends on DNS |

## Key Exam Patterns

- NSG = allow/deny traffic.
- UDR = control route path.
- Bastion = secure VM access without public VM IPs.
- Service endpoint = selected-subnet access to public PaaS endpoint.
- Private endpoint = private IP for PaaS resource.
- Effective security rules = final applied NSG view.
- IP flow verify = allowed/denied traffic check.
- Connection Monitor = ongoing connectivity monitoring.
