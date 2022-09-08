# LDAP

## Manual Enumeration

Even without credentials, you can always query the RootDSE for naming contexts and potentially other information, such as the DnsHostName:

```
ldapsearch -x -h IP_ADDRESS_HERE -b "" -s base
```

Once you have the naming context(s), you can dump them (in this example, the naming context is `dc=cascade,dc=local`):

```
ldapsearch -h IP_ADDRESS_HERE -x -b "DC=cascade,DC=local" 
```

_Note: The output of this ldapsearch contains **more information** than the `ldap-search` nmap script. For example, in HTB cascade, it displayed info about users on the machine while `ldap-search` did not._

## Dumping LDAP

Use ldapdomaindump (with credentials):

```
ldapdomaindump intelligence.htb -u 'intelligence.htb\Tiffany.Molina' -p NewIntelligenceCorpUser9876
```
