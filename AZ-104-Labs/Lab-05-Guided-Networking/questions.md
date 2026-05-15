# Lab 05 — Hard AZ-104 Networking Question Block

## Purpose

These questions reinforce the core networking patterns from Lab 05:

```text
VNet vs subnet
NSG vs UDR
Bastion vs public IP
Service endpoint vs private endpoint
Private DNS
Load Balancer components
Network Watcher troubleshooting
```

## Questions

### Q1

A company hosts web servers and API servers in the same Azure VNet. The web servers must accept HTTP traffic from the internet. The API servers must only accept traffic from the web servers.

What should you use to separate the web and API servers?

A. Two resource groups  
B. Two subnets  
C. Two Azure DNS zones  
D. Two public IP addresses  

**Answer:** B  
**Explanation:** Subnets are the correct network segmentation boundary inside a VNet. Resource groups are management boundaries, not traffic boundaries.

### Q2

You need to allow HTTP traffic to VMs in `snet-web` but block direct internet traffic to VMs in `snet-api`.

Which Azure feature should you configure?

A. NSG  
B. UDR  
C. Azure Policy  
D. Private DNS zone  

**Answer:** A  
**Explanation:** NSGs allow or deny traffic based on source, destination, protocol, and port.

### Q3

You need to force outbound internet traffic from `snet-web` through a firewall appliance in another subnet.

Which feature should you configure?

A. NSG rule  
B. Route table with a user-defined route  
C. Private endpoint  
D. Azure Bastion  

**Answer:** B  
**Explanation:** UDRs control the next hop. NSGs filter traffic but do not redirect it.

### Q4

A VM cannot reach another VM in a peered VNet. NSG rules appear correct. You need to check which route Azure is using.

Which tool should you use?

A. IP flow verify  
B. Effective security rules  
C. Network Watcher Next hop  
D. Azure Advisor  

**Answer:** C  
**Explanation:** Next hop shows the route Azure selects for traffic from a source NIC to a destination IP.

### Q5

You need to check whether TCP 443 from VM1 to VM2 is allowed or denied by NSG rules.

Which tool should you use?

A. Network Watcher IP flow verify  
B. Network Watcher Next hop  
C. Azure DNS  
D. Connection Monitor only  

**Answer:** A  
**Explanation:** IP flow verify checks whether a specific flow is allowed or denied by NSG rules.

### Q6

You create a private endpoint for a storage account. Public network access is disabled. VMs still cannot connect using the normal storage FQDN.

What is the most likely missing configuration?

A. Public IP address  
B. Private DNS zone integration  
C. Azure Bastion  
D. ReadOnly resource lock  

**Answer:** B  
**Explanation:** Private endpoints need correct private DNS so the normal FQDN resolves to the private endpoint IP.

### Q7

A storage account must be reachable using a private IP address from a VNet. Public access should be disabled.

What should you configure?

A. Service endpoint  
B. Private endpoint  
C. Public IP prefix  
D. Application Security Group  

**Answer:** B  
**Explanation:** Private endpoint gives the PaaS service a private IP inside the VNet.

### Q8

A storage account should remain on its public endpoint, but only `snet-web` should be allowed to access it.

What should you configure?

A. Service endpoint on `snet-web` and a storage firewall VNet rule  
B. Private endpoint only  
C. Azure Bastion  
D. Load Balancer inbound NAT rule  

**Answer:** A  
**Explanation:** Service endpoints allow selected subnet access to the Azure PaaS public endpoint.

### Q9

Administrators need SSH/RDP access to private VMs from the Azure portal. The VMs must not have public IP addresses.

What should you deploy?

A. Azure Bastion  
B. Public Load Balancer  
C. Private endpoint  
D. Azure DNS public zone  

**Answer:** A  
**Explanation:** Bastion provides secure portal-based RDP/SSH to VMs over private IP.

### Q10

Is the Bastion public IP the same as the public Load Balancer frontend IP?

A. Yes, both are used for all inbound access  
B. Yes, Bastion forwards user traffic to backend pools  
C. No, Bastion public IP is for admin access; Load Balancer public IP is for application traffic  
D. No, because Bastion does not use public IPs  

**Answer:** C  
**Explanation:** Bastion and Load Balancer are separate resources with separate public IPs and separate purposes.

### Q11

A public Standard Load Balancer distributes TCP 80 traffic to two backend VMs. Users report the site is unavailable.

Which sequence should you check?

A. Tags -> locks -> budgets -> Advisor  
B. Frontend IP -> rule -> health probe -> backend pool -> VM service -> NSG  
C. Private DNS -> Key Vault -> SAS token -> lifecycle rule  
D. VNet peering -> SSPR -> RBAC -> subscription lock  

**Answer:** B  
**Explanation:** Load Balancer troubleshooting follows the traffic chain from frontend to backend health and filtering.

### Q12

You need a single public IP to distribute TCP traffic to multiple VMs. No Layer 7 routing or WAF is required.

Which service should you use?

A. Azure Load Balancer  
B. Application Gateway  
C. Azure Bastion  
D. Private endpoint  

**Answer:** A  
**Explanation:** Azure Load Balancer is Layer 4 and works with TCP/UDP traffic.

### Q13

You need path-based routing for HTTP traffic and WAF protection.

Which service is more appropriate?

A. Azure Load Balancer  
B. Application Gateway  
C. Azure Bastion  
D. UDR  

**Answer:** B  
**Explanation:** Application Gateway is Layer 7 and supports HTTP routing and WAF. Load Balancer is Layer 4.

### Q14

You have an NSG on a subnet and another NSG on a VM NIC. A traffic flow is allowed by the subnet NSG but denied by the NIC NSG.

What is the result?

A. Allowed, because subnet NSG takes priority  
B. Allowed, because allow rules override deny rules  
C. Denied, because both subnet and NIC NSGs must allow the traffic  
D. Allowed only if the VM has a public IP  

**Answer:** C  
**Explanation:** When both subnet and NIC NSGs apply, traffic must be allowed by both effective rule sets.

### Q15

You need to group several changing API VM NICs so they can be referenced in NSG rules without maintaining private IP addresses.

What should you use?

A. Application Security Group  
B. Azure DNS zone  
C. Route table  
D. Management group  

**Answer:** A  
**Explanation:** ASGs group NICs logically for NSG rules.

### Q16

Two VNets have overlapping address spaces. You need private communication between them.

Can you configure VNet peering?

A. Yes, overlapping address spaces are allowed  
B. Yes, but only with Azure Bastion  
C. No, peered VNets cannot have overlapping address spaces  
D. No, VNet peering only works across regions  

**Answer:** C  
**Explanation:** VNet peering requires non-overlapping address spaces.

### Q17

A VM in `vnet-app` needs to resolve a private endpoint DNS record. The private DNS zone exists, but name resolution still returns a public IP.

What should you check?

A. Whether the private DNS zone is linked to `vnet-app`  
B. Whether a CanNotDelete lock exists  
C. Whether the VM has Contributor role  
D. Whether Azure Advisor has recommendations  

**Answer:** A  
**Explanation:** The VNet must be linked to the private DNS zone for clients in that VNet to resolve private endpoint records.

### Q18

A route table has a route:

```text
0.0.0.0/0 -> Virtual appliance 10.60.1.4
```

What does this route do?

A. Allows all inbound traffic  
B. Sends default traffic to the virtual appliance  
C. Blocks all outbound traffic  
D. Creates a private endpoint  

**Answer:** B  
**Explanation:** A `0.0.0.0/0` UDR controls the default route and sends matching traffic to the specified next hop.

### Q19

You need to know all NSG rules that effectively apply to a VM NIC.

Which tool should you use?

A. Effective security rules  
B. Next hop  
C. Cost Management  
D. Azure Backup reports  

**Answer:** A  
**Explanation:** Effective security rules show the combined NSG rules affecting a NIC.

### Q20

You need ongoing connectivity monitoring between a VM and a private endpoint.

Which tool should you use?

A. Connection Monitor  
B. Azure Policy  
C. Blob lifecycle management  
D. Resource Health only  

**Answer:** A  
**Explanation:** Connection Monitor tracks connectivity over time.

## Lab 05 Mental Model

```text
NSG = allow or deny traffic
UDR = choose where traffic goes
Bastion = admin access to private VMs
Load Balancer = user/app traffic to backend VMs
Service endpoint = selected subnet to PaaS public endpoint
Private endpoint = private IP for PaaS
Private DNS = private endpoint works by normal name
IP flow verify = NSG allow/deny test
Next hop = route path test
Effective security rules = all NSG rules on NIC
Connection Monitor = ongoing reachability
```
