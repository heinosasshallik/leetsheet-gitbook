---
description: Simple Network Management Protocol
---

# SNMP

SNMP runs on UDP 161. You can get information about a system from it. But you need to know the **community string** for it to give you a response.&#x20;

Brute forcing the community string:&#x20;

```
onesixtyone -c /usr/share/metasploit-framework/data/wordlists/snmp-default-pass.txt
```

_Note: You will likely want to find a better wordlist._

Getting the data dump:

```
snmpwalk -Os -v1 -c > snmpout.txt
```

Flags:

* `-v1` specifies SNMP version 1

This also gives some (but less) info:&#x20;

```
Metasploit -> auxiliary/scanner/snmp/snmp_enum
```

Things to grep from the datadump:&#x20;

* `System uname`
* `.1.3.6.1.2.1.1.1.0` - [System's hardware type, software operating-system, and networking software.](https://oidref.com/1.3.6.1.2.1.1.1)
* `trap` - To find other community strings (under "traphost")
* `fail` - Finding failed login attempts from logs (telnet or ssh for example, not all devices log these login attempts but some do).&#x20;

Getting ipv6 addresses (if any) from the data dump:&#x20;

```
python enyx.py version communitystring IP
```

{% embed url="https://github.com/trickster0/Enyx" %}

Unique local (Link Local/Local Unicast) is probably the output you’re looking for. It will return loopback as well afaik.
