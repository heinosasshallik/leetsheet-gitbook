# LDAP

## Manual Enumeration

Even without credentials, you can always query the RootDSE for naming contexts and potentially other information, such as the DnsHostName:

```
ldapsearch -x -H ldap://IP_ADDRESS_HERE -b "" -s base
```



## Dumping LDAP

Use ldapdomaindump (with credentials):

```
ldapdomaindump intelligence.htb -u 'intelligence.htb\Tiffany.Molina' -p NewIntelligenceCorpUser9876
```
