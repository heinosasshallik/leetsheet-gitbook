---
description: Techniques for stealing and abusing NTLM credentials
---

# NTLM

## Pass The Hash

The NTLM hash of a user’s password is used in the NTLM challenge-response authentication protocol. Therefore, if you know the user’s NTLM hash, you can impersonate that user for services that rely on NTLM challenge-response.

To find exact commands, look for an article for the specific service you want to pass the hash to. [SMB article](smb.md#pass-the-hash), for example.

## LLMNR/NBT-NS Poisoning&#x20;

If a DNS server doesn’t know the location of something, then an LLMNR / NBT-NS query is sent out over the local network. For example, this can happen when the user mistakenly writes `//pintserver` instead of `//printserver`. These queries are meant for identifying hosts when DNS fails.

An attacker can listen and respond and respond to the victim to send the request to the attacker. The victim's computer then sends out the victim's credentials for authentication to the desired service. The resulting NTLM hash can be cracked or used for pass the hash.

A good tool for this is Responder:

{% embed url="https://github.com/SpiderLabs/Responder" %}

## NTLM Relaying

If you (for example) have MitM with a client, and that client is trying to connect to some resource using the NTLM protocol, then you can relay the authentication messages and connect to it yourself, instead of the client.

NTLM is cross-protocol. For example, in HTTP, the NTLM authentication messages are sent within the “Authorization” header. An attacker can take these messages out of the HTTP header and use them instead in SMB, for example.

NTLM is supported in several protocols, including SMB, HTTP(S), LDAP, IMAP, POP3, MSSQL.

You can get NTLM traffic in several ways

* Traffic to hosts for which the IP is resolved in an insecure manner
  * When the client is configured for DNS servers that don’t exist anymore
  * NBT-NS and LLMNR poisoning
* Traffic resulting from the abuse of AutoDiscovery protocols (WPAD)
  * WPAD is Windows Proxy Auto Detection. Looks for a hostname called WPAD via DNS, and if not successful, via LLMNR and NBNS, allowing for attacks. Several things about this were patched by Microsoft in June 2016 but I guess older versions are still vulnerable
* Traffic which is obtained through a man-in-the-middle attack
  * Arp spoofing
  * Intercepting non-TLS traffic (using ARP spoofing for example), then redirecting this traffic to a location that the victim’s workstation trusts. If Automatic Intranet Detection is enabled (default), then the client will automatically authenticate (to SMB for example, if I understood correctly)

Use ntlmrelayx for this. Here’s a good blog post detailing how it’s done:

{% embed url="https://www.fox-it.com/en/insights/blogs/blog/inside-windows-network/" %}
