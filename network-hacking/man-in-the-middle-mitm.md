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

## WPAD&#x20;



WPAD is Windows Proxy Auto Detection. Looks for a hostname called WPAD via DNS, and if not successful, via LLMNR and NBNS, allowing for attacks. Several things about this were patched by Microsoft in June 2016 but I guess older versions are still vulnerable

Steps:

1. If the DHCP Server is configured, the client retrieves the wpad.dat file from the DHCP Server (if successful, step 4 is taken)
2. The wpad.corpdomain.com query is sent to the DNS server to find the device that is distributing the Wpad configuration. (If successful, step 4 is taken)
3. Sent LLMNR query for WPAD (if success, go step 4 else proxy can’t be use)
4. Download wpad.dat and use

So, DHCP poisoning, DNS poisoning, or LLMNR poisoning can be used to get to step 4. Plus, (probably patched since 2016) if WPAD prompts for authentication, the workstation would send its NTLM.

This allows you to MITM.

[Responder](https://github.com/lgandx/Responder) is a tool that serves a fake WPAD server and responds to clients’ WPAD name resolution. The client gets served `wpad.dat` from the server. Responder creates a fake authentication screen asking for the username and password the users use in the domain. If the employee writes in their username and password, then that’s very nice.

TODO: Link phishing page to here

Responder can be used for more than that though. It can also force users to download malicious files by directing them to a fake web page.&#x20;

Example is here:

{% embed url="https://pentest.blog/what-is-llmnr-wpad-and-how-to-abuse-them-during-pentest/" %}

\


Mitigation: disable “auto detect proxy” on browser.
