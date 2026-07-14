# Active Directory Replication

Before understanding DCSync, it is important to understand how Active Directory replication works.

In a Windows domain, every Domain Controller maintains a copy of the Active Directory database (`NTDS.dit`).

Whenever an administrator:

- Creates a user
- Changes a password
- Modifies a group
- Resets an account
- Updates permissions

those changes must be replicated to every Domain Controller to keep the domain synchronized.

## How Replication Works

Instead of manually copying the database, Domain Controllers communicate through Microsoft's **Directory Replication Service (DRS)**.

This process allows trusted Domain Controllers to exchange directory information automatically.

## Why Is This Important?

DCSync abuses this legitimate feature.

Instead of exploiting a vulnerability, an attacker impersonates a trusted Domain Controller and requests replication data.

If the account has replication rights, Windows treats the request as legitimate and returns credential information.

The attack succeeds because of excessive privileges—not because Active Directory is vulnerable.

## Key Takeaways

- Active Directory relies on replication to function correctly.
- Replication is performed using Microsoft's DRS protocol.
- Only accounts with replication permissions should perform this operation.
- DCSync abuses legitimate replication functionality to retrieve credentials.
