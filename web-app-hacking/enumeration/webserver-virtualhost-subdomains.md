# Webserver Virtualhost Subdomains

You can use a web fuzzer to enumerate whether the web server is configured with any subdomains. Change the "Host" header and see if the website responds with something different.

For example, to enumerate subdomains of `*.bart.htb`, you can do:

```text
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -H "HOST:FUZZ.bart" -u http://bart:80 2>&1 
```







