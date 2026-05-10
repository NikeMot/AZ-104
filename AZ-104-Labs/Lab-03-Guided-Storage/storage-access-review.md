# Lab 03 Storage Access Review

## Access Keys

Access keys were reviewed as broad account-level secrets.

### Exam lesson

Access keys should not be shared for temporary or limited access. They provide broad access and should be protected like credentials.

## SAS Token

A SAS token was created or reviewed for temporary delegated access.

### Key points

- SAS should be scoped to the required resource.
- SAS should include only required permissions.
- SAS should have a limited expiry.
- SAS should use HTTPS where possible.

### Exam lesson

If the requirement says temporary limited access, choose SAS instead of account keys.

## Stored Access Policy

A stored access policy was configured or reviewed for container-level SAS management.

### Exam lesson

A stored access policy allows SAS permissions and expiry to be managed centrally. It is useful when SAS access may need to be revoked or adjusted without recreating every issued SAS.

## Network Access

Storage network restrictions were configured or reviewed using storage firewall and virtual network rules.

### Exam lesson

Network access and identity access are separate. A user can have the right permission but still be blocked by storage firewall settings.

## Azure Files Identity-Based Access

Identity-based access options for Azure Files were reviewed.

Possible options include:

- Active Directory Domain Services
- Microsoft Entra Domain Services
- Microsoft Entra Kerberos, where supported

### Exam lesson

Azure Files can support identity-based SMB access. This is preferred when users or groups need access using identity rather than shared storage account keys.

## Access Decision Table

| Requirement | Correct storage access method |
|---|---|
| Temporary read/list access to blobs | SAS token |
| Revoke SAS centrally | Stored access policy |
| Full account-level administrative secret | Access key |
| Restrict storage to selected networks | Storage firewall/VNet rule |
| User/group access to Azure Files | Identity-based Azure Files access |
