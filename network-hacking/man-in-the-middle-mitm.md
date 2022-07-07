# Man-In-the-Middle (MITM)

## SSLStrip

If you have already achieved MiTM, then you can attempt to steal credentials by stripping the HTTPS off sites. When the victim tries to connect, you establish an HTTPS connection to the site while passing unencrypted HTTP to the victim.

This is mitigated by HSTS.

## Evil Twin

You can use a WiFi Pineapple to pretend to be a wifi access point. If clients connect to it, then you can MiTM sites.

## ARP Spoofing

The ARP protocol is insecure and you can get MITM by ARP spoofing to indicate that the IP of a machine has the MAC of our device.

## DNS Takeover With mitm6

mitm6 is a tool that exploits the default configuration of Windows to take over the default DNS server. It does this by replying to DHCPv6 messages, providing the victim a IPv6 address and setting the attacker as default DNS server.&#x20;

For a full explanation of the attack, see the[ blog about mitm6](https://blog.fox-it.com/2018/01/11/mitm6-compromising-ipv4-networks-via-ipv6/). Mitm6 is designed to work together with[ ntlmrelayx from impacket](https://github.com/CoreSecurity/impacket) for WPAD spoofing and credential relaying.
