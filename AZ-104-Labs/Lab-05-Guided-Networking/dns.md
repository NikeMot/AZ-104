# Lab 05 — Azure DNS and Private DNS Notes

## Why this file exists

The original Lab 05 walkthrough covered private endpoint DNS only briefly. That was not enough for the AZ-104 networking objective because DNS is a core part of Azure networking design.

This file explains the DNS part of the Lab 05 architecture clearly.

## DNS objective covered

**AZ-104 domain:** Implement and manage virtual networking  
**Objective:** Configure Azure DNS

In this lab, DNS appears in two ways:

1. **Public DNS / Azure DNS public zones** — used when internet clients need to resolve public names.
2. **Private DNS zones** — used when resources inside VNets need to resolve private names, especially private endpoints.

## The key idea

Networking is not only IP addresses and routes. Applications usually connect by name.

For example, an app usually connects to Storage using a name like:

```text
mystorageaccount.blob.core.windows.net
```

If that name resolves to a public IP, traffic goes toward the public Storage endpoint.

If that name resolves to a private endpoint IP, traffic stays private inside the VNet path.

## Where DNS fits in the Lab 05 architecture

```text
Application VM
   |
   | asks DNS for mystorageaccount.blob.core.windows.net
   v
Private DNS zone linked to vnet-app
   |
   | returns private endpoint IP
   v
Private endpoint in snet-private-endpoints
   |
   v
Storage account blob service
```

The private endpoint gives Storage a private IP.

The private DNS zone makes the normal Storage FQDN resolve to that private IP.

Both are required for a clean private endpoint design.

## Public DNS vs Private DNS

| Requirement | Correct DNS feature |
|---|---|
| Internet users need to resolve `www.contoso.com` to a public IP | Azure DNS public zone |
| VMs inside a VNet need to resolve private records | Azure Private DNS zone |
| Private endpoint should work with the normal service FQDN | Azure Private DNS zone for the correct `privatelink` namespace |
| Multiple VNets need to resolve the same private endpoint records | Link the private DNS zone to each required VNet |

## Private endpoint DNS pattern

For Azure Storage Blob private endpoints, the private DNS zone is normally:

```text
privatelink.blob.core.windows.net
```

The normal public FQDN might be:

```text
mystorageaccount.blob.core.windows.net
```

With private DNS correctly configured, clients in the linked VNet resolve the normal service name to the private endpoint IP.

Expected result:

```text
mystorageaccount.blob.core.windows.net -> private endpoint IP
```

Not:

```text
mystorageaccount.blob.core.windows.net -> public Storage IP
```

## Why private endpoint can fail even when the endpoint exists

A private endpoint creates the private IP path, but DNS decides whether clients use it.

If DNS is wrong, the app may still try the public endpoint.

This is a common AZ-104 trap:

```text
Private endpoint exists.
Public access is disabled.
Client still resolves public IP.
Connection fails.
```

The likely fix is:

```text
Configure the correct private DNS zone and link it to the VNet.
```

## Portal steps — private DNS for private endpoint

When creating a private endpoint in the Azure portal:

1. Open the target PaaS resource, such as a Storage account.
2. Go to **Networking**.
3. Select **Private endpoint connections**.
4. Create a private endpoint.
5. Choose the correct sub-resource, for example `blob`.
6. Choose the VNet and subnet, for example:

```text
vnet-app / snet-private-endpoints
```

7. In the DNS section, enable private DNS integration.
8. Azure creates or uses the correct private DNS zone.
9. Azure links the private DNS zone to the VNet.
10. Azure creates the DNS record for the private endpoint.

## Portal steps — check private DNS zone

1. Search for **Private DNS zones**.
2. Open the zone, for example:

```text
privatelink.blob.core.windows.net
```

3. Check **Recordsets**.
4. Confirm an A record exists for the Storage account.
5. Go to **Virtual network links**.
6. Confirm `vnet-app` is linked.

## CLI validation

From a VM in the linked VNet, test name resolution:

```bash
nslookup <storage-account-name>.blob.core.windows.net
```

Expected result:

```text
The result should resolve to the private endpoint IP address.
```

If it resolves to a public IP, check:

```text
Private DNS zone exists
Correct privatelink zone name is used
A record exists
VNet link exists
Client VM is in a linked VNet
Custom DNS servers forward Azure private DNS correctly if custom DNS is used
```

## DNS and VNet peering

VNet peering connects networks, but it does not automatically make all DNS work everywhere.

If a private DNS zone is linked only to `vnet-app`, then resources in `vnet-shared` may not resolve the private endpoint name unless:

```text
The private DNS zone is also linked to vnet-shared
or
custom DNS forwarding is configured correctly
```

Exam trap:

```text
Peering gives network reachability.
DNS still needs proper zone links or forwarding.
```

## DNS and Load Balancer

The public Load Balancer has a public IP. If users need a friendly name such as:

```text
app.contoso.com
```

then a public DNS record can point to the Load Balancer frontend public IP.

That is separate from private endpoint DNS.

```text
Public app DNS -> Load Balancer public IP
Private endpoint DNS -> private endpoint IP
```

Do not mix them up.

## DNS and Bastion

Bastion has a public IP for administrator access through the Azure portal.

You normally do not use Bastion as the public DNS target for the application.

```text
Bastion public IP = admin access
Load Balancer public IP = application access
Private DNS = private endpoint/internal name resolution
```

## Exam patterns

| Exam wording | Think |
|---|---|
| Public users need to resolve a domain to an Azure public IP | Azure DNS public zone / public DNS record |
| Private endpoint exists but FQDN resolves to public IP | Private DNS zone or VNet link missing |
| Storage account must use private IP while apps keep normal FQDN | Private endpoint + private DNS |
| Peered VNet cannot resolve private endpoint name | Link private DNS zone to that VNet or configure DNS forwarding |
| DNS record should only be resolvable inside VNets | Azure Private DNS zone |

## Memory cue

```text
Private endpoint gives the private IP.
Private DNS makes the name use that private IP.
VNet link tells which VNets can resolve the private record.
```

## What I should be able to explain

After Lab 05, I should be able to explain:

- what Azure DNS public zones are for
- what Azure Private DNS zones are for
- why private endpoint DNS matters
- why private endpoint connectivity can fail by FQDN
- why VNet peering does not automatically solve DNS
- why Bastion, Load Balancer, and private endpoint DNS are separate concepts
