---
description: Get hostnames and info from DNS servers
---

# Domains

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

## AltDNS

AltDNS is a useful tool for enumerating subdomains. You can use subdomains you already know about and then apply changes and permutations to them to try to discover new ones.

{% embed url="https://github.com/infosec-au/altdns" %}

## DNSDumpster

[https://dnsdumpster.com/](https://dnsdumpster.com/)

Queries DNS servers and returns subdomains it finds. Here’s the explanation about how it works: [https://dnsdumpster.com/footprinting-reconnaissance/](https://dnsdumpster.com/footprinting-reconnaissance/)

## Autonomous System \(AS\) Numbers

Finding Autonomous System \(AS\) Numbers will help us identify netblocks belonging to an organization which in-turn may have valid domains.

1. Resolve the IP address of a given domain using dig or host
2. There are tools to find ASN given an IP address — https://asn.cymru.com/cgi-bin/whois.cgi
3. There are tools to find ASN given a domain name — http://bgp.he.net/
4. Finding AS Number using IP address
5. The ASN numbers found can be used to find netblocks of the domain. There are Nmap scripts to achieve that — https://nmap.org/nsedoc/scripts/targets-asn.htm

```text
nmap --script targets-asn --script-args targets-asn.asn=17012
```

## Zone Transfers

If zone transfers are enabled, you can pull all the DNS data from a nameserver:

```text
dig +multi AXFR @ns1.insecuredns.com insecuredns.com
```

## Zone Walking

You can try zone walking if they have NSEC.

What it is: 

[http://info.menandmice.com/blog/bid/73645/Take-your-DNSSEC-with-a-grain-of-salt](http://info.menandmice.com/blog/bid/73645/Take-your-DNSSEC-with-a-grain-of-salt)

Tool usage:

```text
ldns-walk @ns1.insecuredns.com insecuredns.com
```



## ForwardDNS

There’s a huge database called Forward DNS that’s been compiled. You can access it on scans.io’s website I think? It’s supposed to be pretty thorough.

```text
curl -silent https://scans.io/data/rapid7/sonar.fdns_v2/20170417-fdns.json.gz | pigz -dc | grep ".icann.org" | jq
```

The database is 19GB compressed and 300GB uncompressed though. You’ll have to download it and uncompress it so make sure you have a good internet and lots of disk space.







