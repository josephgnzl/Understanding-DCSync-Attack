# Required Replication Permissions

Not every domain user can perform a DCSync attack.

To request replication data from a Domain Controller, an account must have specific Active Directory replication permissions.

These permissions are normally assigned to Domain Controllers and highly privileged administrative groups. However, they are sometimes delegated to service accounts, backup solutions, or third-party applications, creating an opportunity for attackers.

## Required Permissions

An account must have the following permissions over the domain object:

- Replicating Directory Changes
- Replicating Directory Changes All
- Replicating Directory Changes In Filtered Set

Together, these permissions allow an account to request Active Directory replication data, including password hashes.

## Who Usually Has These Permissions?

The following groups typically possess replication rights by default:

- Domain Controllers
- Domain Admins
- Enterprise Admins

In some environments, delegated service accounts may also receive these permissions to support synchronization or backup operations.

## Why Is This Dangerous?

If an attacker compromises an account with replication privileges, they can impersonate a Domain Controller and request credential data without accessing the NTDS.dit database or dumping LSASS.

Windows considers the request legitimate because the account is authorized to replicate directory information.

## How Can We Identify These Permissions?

During an Active Directory assessment, replication rights can be identified using tools such as:

- BloodHound
- PowerView
- PowerShell
- Active Directory Users and Computers (Advanced Features)

BloodHound is especially useful because it visualizes privilege relationships and quickly highlights accounts capable of performing a DCSync attack.
