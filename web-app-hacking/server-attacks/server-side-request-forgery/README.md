---
description: SSRF / Server Side Request Forgery
---

# Server Side Request Forgery

Server-side request forgery (also known as SSRF) is a web security vulnerability that allows an attacker to induce the server-side application to make HTTP requests to an arbitrary domain of the attacker's choosing. This allows you to:

* Make requests to internal services that you wouldn't be able to interact with otherwise.
* Force the server to connect to arbitrary external systems, potentially leaking sensitive data such as authorization credentials.

This can even lead to RCE when the SSRF allows you to interact with certain services that outsiders aren't supposed to be able to access (e.g Redis in certain cases).

## Tricks

### Use DNS to Access Internal IP Addresses

If the IP address 127.0.0.1 is blocked, then you might be able to get around that by making the request to your-malicious-dns.com and your DNS will resolve the hostname to 127.0.0.1.

You don't even have to pay to do this. There are a number of "wildcard DNS" services, such as [xip.io](https://ourcodeworld.com/articles/read/1510/xip-io-a-magic-domain-name-that-provides-wildcard-dns-for-any-ip-address), that can be used to resolve a hostname to an internal IP address.

### IPv6 to IPv4 Mapping

Ipv6 maps to ipv4 with a certain prefix (`::ffff:<ipv4>`). So if localhost (`127.0.0.1`) is blocked, then `::ffff:127.0.0.1` might not be.

### Protocol Smuggling

You can send a HTTP request to a non-HTTP text-based service. In the likely scenario that invalid commands get thrown out without invalidating the entire interaction, you will be able to smuggle valid text-based commands in the middle of the HTTP request. Therefore, you can interact with non-HTTP services

HTTP based protocols:

* Elastic
* CouchDB
* MongoDB
* Docker

Text-based protocols:

* FTP
* SMTP
* Redis
* Memcached

If **gopher** is enabled, then that can make your life really easy, but it's usually not.

However, often, controls have been put in place to try to prevent protocol smuggling. To read about how to circumvent these controls, read about [CRLF Injection](./#crlf-injection).&#x20;

### CRLF Injection

Often, controls have been put in place to try to prevent protocol smuggling. CRLF Injection is one way to overcome that.

#### CRLF Injection in HTTPS

[https://www.blackhat.com/docs/us-17/thursday/us-17-Tsai-A-New-Era-Of-SSRF-Exploiting-URL-Parser-In-Trending-Programming-Languages.pdf](https://www.blackhat.com/docs/us-17/thursday/us-17-Tsai-A-New-Era-Of-SSRF-Exploiting-URL-Parser-In-Trending-Programming-Languages.pdf)

You can’t smuggle SMTP over HTTP, because servers won’t accept `http://` requests. It will cut off the connection. But you can smuggle it over HTTPS, because of the TLS handshake.

The Server Name Indication isn’t encrypted in a TLS handshake. If you put a space there, then you can smuggle an SMTP request. This works because of the way Linux’s glibc works. I think normally the after the space part is supposed to be metadata/comment or something.

```
https://127.0.0.1 %0D%0AHELO orange.tw%0D%0AMAIL FROM…:25/
```

Before the space is HTTP, and after the space is an SMTP request we smuggled. You should test this using:

![](https://lh4.googleusercontent.com/D5zHpOMsEVbb5bR5QAhGrC\_PIAlOeuXE\_jnbcWr6RbpHMhCwCaNV1rAruf9MRfNDABQnnLs3hTCTBbHVpmaFaJ0gHTbcFrDIgYagPdYt-jASMx9pCPHCvdXPl384NPuxP1Cgi2jF)

### URL Parsing Issues

Fantastic talk on how URL parsers can be tricked into doing weird things: [https://www.blackhat.com/docs/us-17/thursday/us-17-Tsai-A-New-Era-Of-SSRF-Exploiting-URL-Parser-In-Trending-Programming-Languages.pdf](https://www.blackhat.com/docs/us-17/thursday/us-17-Tsai-A-New-Era-Of-SSRF-Exploiting-URL-Parser-In-Trending-Programming-Languages.pdf)

Parsing the URL correctly is difficult. There's an RFC for it, but some libraries still do it differently. Issues can arise when there's inconsistency between components that parse URLs differently. For example, when one component verifies an URL and then another one makes a request to it. If the two components parse the URL differently, then you likely have an SSRF vulnerability.
