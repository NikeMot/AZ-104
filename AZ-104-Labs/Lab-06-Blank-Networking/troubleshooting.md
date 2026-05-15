# Lab 06 Troubleshooting Notes

## Troubleshooting Approach

This lab used a from-scratch network design, so troubleshooting had to follow the architecture rather than a checklist from instructions.

The correct method is:

```text
1. Confirm topology.
2. Confirm DNS.
3. Confirm route path.
4. Confirm NSG filtering.
5. Confirm service/backend health.
6. Confirm guest OS/application behavior.
```

## If VNet Peering Fails

Check:

```text
Application VNet address space does not overlap shared-services VNet.
Peering exists in both directions.
Peering state is Connected.
Allow virtual network access is enabled.
NSGs do not block the intended private flow.
UDRs do not send the traffic to an invalid next hop.
DNS is separately handled if name resolution is involved.
```

Exam lesson:

```text
Peering enables private connectivity, but it does not override NSGs, UDRs, or DNS design.
```

## If Web Traffic Fails

Check this chain:

```text
Public DNS record if used
Load Balancer frontend public IP
Load balancing rule
Health probe
Backend pool membership
Backend VM service listening on the correct port
NSG rules
Guest OS firewall
```

Exam lesson:

```text
Load Balancer requires frontend IP, rule, backend pool, probe, healthy backend service, and allowed traffic path.
```

## If API Tier Is Reachable From the Internet

Check:

```text
Does any API VM have a public IP?
Is the API subnet NSG too permissive?
Is the API reachable through the web frontend path only?
Are ASGs or source prefixes too broad?
Is there an unintended public Load Balancer or NAT rule?
```

Exam lesson:

```text
Private backend tiers should not have direct public exposure.
```

## If Private Endpoint DNS Fails

Check:

```text
Private DNS zone exists.
Correct privatelink namespace is used.
A record exists for the private endpoint.
Private DNS zone is linked to the application VNet.
Client VM is in a linked VNet.
Custom DNS servers forward correctly if used.
```

Exam lesson:

```text
Private endpoint gives the private IP. Private DNS makes the normal FQDN use that private IP.
```

## If Bastion Cannot Connect

Check:

```text
Subnet is named exactly AzureBastionSubnet.
Bastion deployment completed successfully.
Bastion has its own public IP.
Target VM has private IP connectivity from the Bastion VNet.
NSG allows required private management path.
The VM is running.
Credentials or VM login permissions are valid.
```

Exam lesson:

```text
Bastion is for admin access to private VMs. It is not the application frontend.
```

## If UDR Path Is Wrong

Check:

```text
Route table is associated with the correct subnet.
Destination prefix matches the traffic.
More specific routes are not overriding the default route.
Next hop type is correct.
Virtual appliance IP is reachable.
Effective routes show the expected path.
```

Exam lesson:

```text
UDR controls route path. It does not allow or deny traffic by itself.
```

## If Load Balancer Backends Are Unhealthy

Check:

```text
Backend VMs are in the backend pool.
Health probe protocol and port match the service.
Service is running on backend VMs.
NSG allows probe and frontend traffic.
Guest OS firewall allows the backend port.
Load balancing rule references the correct frontend, backend pool, and probe.
```

Exam lesson:

```text
If the probe fails, the backend is removed from rotation.
```

## Network Watcher Tool Mapping

| Problem | Tool |
|---|---|
| Check whether traffic is allowed or denied by NSG | IP flow verify |
| Check which route Azure uses | Next hop |
| View all effective NSG rules on NIC | Effective security rules |
| View all routes on NIC | Effective routes |
| Monitor connection over time | Connection Monitor |

## Final Troubleshooting Memory Cue

```text
DNS tells the client where to go.
Routes decide the path.
NSGs decide whether the packet is allowed.
Load Balancer decides which healthy backend receives traffic.
Bastion provides admin access.
Guest OS/app must still be listening.
```
