# Lab 04 Storage Access Review

## Access Keys

Access keys were reviewed as broad account-level secrets.

### Why access keys are risky

Access keys can grant broad access to the storage account. They should not be shared when a narrower method such as SAS or identity-based access is suitable.

### Exam lesson

If the requirement asks for temporary or scoped access, do not choose access keys unless broad account-level access is explicitly required.

## SAS Token

SAS was used or reviewed as the correct mechanism for temporary delegated access.

### Key decision points

- Scope the SAS to the required container or blob.
- Use only the required permissions.
- Set a short expiry.
- Use HTTPS only where possible.

### Exam lesson

Temporary contractor access to blobs usually points to SAS.

## Stored Access Policy

Stored access policy was reviewed as the correct option for central SAS management.

### Exam lesson

If several SAS tokens need to be revoked or managed centrally, use a stored access policy.

## Network Access

Storage firewall and VNet/subnet access were configured or reviewed.

### Exam lesson

Network restrictions and identity permissions are separate. Correct RBAC permissions do not guarantee access if the network path is blocked.

## Identity-Based Azure Files Access

Identity-based access for Azure Files was reviewed.

### Exam lesson

Azure Files can support identity-based SMB access. This is better than shared account keys when user/group-based file access is required.

## Exam Decision Table

| Requirement | Correct feature |
|---|---|
| Temporary limited blob access | SAS token |
| Central SAS revocation | Stored access policy |
| Full account-level secret | Access key |
| Restrict access by network | Storage firewall / VNet rule |
| User/group-based Azure Files access | Identity-based Azure Files access |
