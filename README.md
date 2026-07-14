## Understanding-DCSync-Attack

A hands-on guide to understanding and performing the DCSync attack in a controlled Active Directory lab.

This repository explains how Active Directory replication works, why DCSync is one of the most powerful post-exploitation techniques, and demonstrates the attack using Impacket against a Windows Server domain.


## Lab Environment

```
Attacker Machine : Kali Linux
Target           : Windows Server 2022
Role             : Domain Controller
Domain           : RAYNEX.LAB
Tools            : Impacket, PowerView

```
## Attack Chain

```text
Enumeration
      ↓
Privilege Escalation
      ↓
Replication Rights
      ↓
DCSync (secretsdump.py)
      ↓
NTLM Hash Extraction
      ↓
Pass-the-Hash
      ↓
Evil-WinRM
      ↓
Administrative Access
```
