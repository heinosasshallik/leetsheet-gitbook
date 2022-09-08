# LDAP

## Manual Enumeration

You can always query the RootDSE for naming contexts and and other information (such as authentication info). Refer to the following to get the naming context and dump information:

{% embed url="https://book.hacktricks.xyz/network-services-pentesting/pentesting-ldap#basic-enumeration" %}

## Dumping LDAP

Use ldapdomaindump (with credentials):

```
ldapdomaindump intelligence.htb -u 'intelligence.htb\Tiffany.Molina' -p NewIntelligenceCorpUser9876
```
