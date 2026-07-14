## Understanding-DCSync-Attack

A hands-on guide to understanding and performing the DCSync attack in a controlled Active Directory lab.

This repository explains how Active Directory replication works, why DCSync is one of the most powerful post-exploitation techniques, and demonstrates the attack using Impacket against a Windows Server domain.

## What is DCSync?

DCSync is an Active Directory attack that abuses the Domain Replication Service (DRS) to request credential data from a Domain Controller.

Instead of dumping credentials from memory or extracting the NTDS.dit database, an attacker impersonates a legitimate Domain Controller and requests replication data through Microsoft's own replication protocol.

If the compromised account has the required replication permissions, the Domain Controller willingly returns password hashes.
