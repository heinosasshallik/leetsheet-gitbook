---
description: General enumeration
---

# Enumeration

## SSH Version

If the machine allows SSH, then looking at the OpenSSH version will give you an idea of when the machine was last updated.&#x20;

Also, if the machine was never updated (like in HackTheBox), then you can match the release date of the OpenSSH version to a Linux version. For example, if the machine is an Ubuntu machine, then you can look at which version of Ubuntu was latest when that release of OpenSSH was latest.

## Port Scanning

Port scanning is an important part of enumerating the services that are running on a network machine.

### Nmap

Normal TCP scan:

```
nmap -sC -sV -p- -vvv hostname_here 
```

UDP scan &#x20;

```
nmap -sU -sC -sV -p- -vvv hostname_here
```

{% embed url="https://hackertarget.com/nmap-cheatsheet-a-quick-reference-guide/" %}

Common flags:

* `-p-` : Scan all ports
* `-vvv` : Maximum verbosity
* `-sV` : Service detection
* `-A` : Detect all things, including services and OS
* `-sC` : Scan using default **safe** scripts
* `-Pn` : Scan a host even if it doesn't respond to pings

Stealth scans:

{% embed url="https://nmap.org/bennieston-tutorial/" %}

Finding nmap scripts:

```
locate *.nse
```
