# DNS Rebinding

It’s a way to get into private networks using the victim’s browser

You have them go to your domain evil.com. You control the DNS server to that domain. Let’s say the IP address is 152.152.152.152

You give them a very short TTL for the DNS record. 

Now that they are on your site, you have them query your site additional times.

Then, when the TTL for the DNS runs out, you give them a new IP for your site, like 10.10.10.15. That means they will make the query to 10.10.10.15, thinking they are querying your server. This allows you to make requests inside their private network, possibly compromising IoT devices and whatnot.



