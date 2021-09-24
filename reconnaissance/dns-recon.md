---
description: Get hostnames and info from DNS servers
---

# DNS Recon

## Dig

If you've identified a DNS nameserver, then you can query that server with [dig](http://securityidiots.com/Web-Pentest/Information-Gathering/Part-4-DNS-information-Gathering-with-DIG.html).

## Fierce

[Fierce](https://github.com/mschwager/fierce) is a DNS reconnaissance tool for locating non-contiguous IP space.

> Fierce is a semi-lightweight scanner that helps locate non-contiguous IP space and hostnames against specified domains. It's really meant as a pre-cursor to nmap, unicornscan, nessus, nikto, etc, since all of those require that you already know what IP space you are looking for. This does not perform exploitation and does not scan the whole internet indiscriminately. It is meant specifically to locate likely targets both inside and outside a corporate network. Because it uses DNS primarily you will often find mis-configured networks that leak internal address space. That's especially useful in targeted malware.

## DNSRecon

Use a dictionary attack to enumerate subdomains against a DNS server.

```bash
python dnsrecon.py -n ns1.insecuredns.com -d insecuredns.com -D subdomains-top1mil-5000.txt -t brt
```





