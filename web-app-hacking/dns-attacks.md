# DNS Attacks

## Dangling Records

{% embed url="https://nakedsecurity.sophos.com/2020/07/07/company-web-names-hijacked-via-outdated-cloud-dns-records/" %}

Let’s say a company sets up a temporary site - julyoffer.company.com - which is only supposed to be active for 1 month and will not be used after that.

Since it’s a temporary site, you might not include it in your main website, but rather make a new microsite. You use the hosting provider `hostingco` and set up a DNS record like so:

```
julyoffer.example.com: alias (CNAME record) -> temp-1234.hostingco.example (cache for 5 mins)
```

When the julyoffer site is taken down, but the DNS record is left dangling, then you might have a problem. If hostingco recycles the temporary cloud names (temp-1234), then an attacker may be able to set up his own site on temp-1234.hostingco.example

In that case, the attacker could take over traffic coming to julyoffer.example.com. He could use that to host malware on a trusted domain, or conduct a phishing campaign.
