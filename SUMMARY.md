# Table of contents

* [Leet Sheet](README.md)
* [TODO](todo.md)

## Reconnaissance

* [Automated Reconnaissance](reconnaissance/automated-reconnaissance.md)
* [Domains](reconnaissance/dns-recon.md)
* [Scour the Web](reconnaissance/google-fu.md)
* [Metadata](reconnaissance/metadata.md)

## Web App Hacking

* [Enumeration](web-app-hacking/enumeration/README.md)
  * [Webserver Virtualhost Subdomains](web-app-hacking/enumeration/webserver-virtualhost-subdomains.md)
  * [Common Identifiers](web-app-hacking/enumeration/common-identifiers.md)
  * [Directory Enumeration](web-app-hacking/enumeration/directory-enumeration/README.md)
    * [Automated Directory Enumeration](web-app-hacking/enumeration/directory-enumeration/automated-directory-enumeration.md)
    * [Manual Directory Enumeration](web-app-hacking/enumeration/directory-enumeration/manual-directory-enumeration.md)
  * [Automated Web Technology Detection](web-app-hacking/enumeration/automated-web-technology-detection.md)
* [Exploitation](web-app-hacking/exploitation/README.md)
  * [User Attacks](web-app-hacking/exploitation/user-attacks/README.md)
    * [CORS Misconfigurations](web-app-hacking/exploitation/user-attacks/cors-misconfigurations.md)
    * [DNS Rebinding](web-app-hacking/exploitation/user-attacks/dns-rebinding.md)
    * [Open Redirect](web-app-hacking/exploitation/user-attacks/open-redirect.md)
    * [Clickjacking](web-app-hacking/exploitation/user-attacks/clickjacking.md)
    * [Cross Site Request Forgery (CSRF)](web-app-hacking/exploitation/user-attacks/cross-site-request-forgery-csrf.md)
    * [Session Fixation](web-app-hacking/exploitation/user-attacks/session-fixation.md)
    * [XSS/Cross Site Scripting](web-app-hacking/exploitation/user-attacks/xss-cross-site-scripting.md)
    * [CSS Injection](web-app-hacking/exploitation/user-attacks/css-injection.md)
    * [HTML Injection](web-app-hacking/exploitation/user-attacks/html-injection.md)
    * [Phishing](web-app-hacking/exploitation/user-attacks/phishing.md)
  * [Database Attacks](web-app-hacking/exploitation/database-attacks/README.md)
    * [SQL Injection](web-app-hacking/exploitation/database-attacks/sql-injection.md)
    * [Get a Shell From DB Connection](web-app-hacking/exploitation/database-attacks/get-a-shell-from-db-connection.md)
  * [Server Attacks](web-app-hacking/exploitation/server-attacks/README.md)
    * [Collisions](web-app-hacking/exploitation/server-attacks/collisions.md)
    * [Server Side Request Forgery](web-app-hacking/exploitation/server-attacks/server-side-request-forgery/README.md)
      * [Redis SSRF](web-app-hacking/exploitation/server-attacks/server-side-request-forgery/redis-ssrf.md)
    * [Insecure Direct Object Reference](web-app-hacking/exploitation/server-attacks/insecure-direct-object-reference.md)
    * [Timing-Based Side-Channel Attacks](web-app-hacking/exploitation/server-attacks/timing-based-side-channel-attacks.md)
    * [Attacking Authentication Methods](web-app-hacking/exploitation/server-attacks/attacking-authentication-methods/README.md)
      * [JWT Attacks](web-app-hacking/exploitation/server-attacks/attacking-authentication-methods/jwt-attacks.md)
      * [Brute Forcing Web Forms](web-app-hacking/exploitation/server-attacks/attacking-authentication-methods/brute-forcing-web-forms.md)
    * [Loose Comparisons](web-app-hacking/exploitation/server-attacks/loose-comparisons.md)
    * [Unrestricted File Upload](web-app-hacking/exploitation/server-attacks/page-3.md)
    * [Insecure Deserialization](web-app-hacking/exploitation/server-attacks/page-2.md)
    * [Command Injection](web-app-hacking/exploitation/server-attacks/page-1.md)
    * [Path Traversal](web-app-hacking/exploitation/server-attacks/path-traversal.md)
    * [File Inclusion](web-app-hacking/exploitation/server-attacks/file-inclusion-todo-complete-this.md)
    * [Server-Side Template Injection](web-app-hacking/exploitation/server-attacks/server-side-template-injection.md)
    * [XML External Entities Injection (XXE)](web-app-hacking/exploitation/server-attacks/page-1-1.md)
    * [Server Misconfigurations](web-app-hacking/exploitation/server-attacks/server-misconfigurations.md)
    * [Parser Inconsistencies](web-app-hacking/exploitation/server-attacks/parser-inconsistencies.md)
    * [Bypassing WAFs](<web-app-hacking/exploitation/server-attacks/page-1-1 (1).md>)
  * [DNS Attacks](web-app-hacking/exploitation/dns-attacks.md)
  * [Cloud Attacks](web-app-hacking/exploitation/cloud-attacks.md)
    * [Amazon Web Services](web-app-hacking/exploitation/cloud-attacks/amazon-web-services.md)
  * [Interesting Outdated Attacks](web-app-hacking/exploitation/interesting-outdated-attacks/README.md)
    * [SQL Truncation](web-app-hacking/exploitation/interesting-outdated-attacks/sql-truncation.md)

## Network Hacking

* [General Enumeration](network-hacking/untitled.md)
* [RPC](network-hacking/rpc.md)
* [LDAP](network-hacking/ldap.md)
* [SMB](network-hacking/smb.md)
* [SNMP](network-hacking/snmp.md)
* [WMI](network-hacking/wmi.md)
* [SSH](network-hacking/ssh.md)
* [Kerberos](network-hacking/kerberos.md)
* [NTLM](network-hacking/ntlm.md)
* [Man-In-the-Middle (MITM)](network-hacking/man-in-the-middle-mitm.md)
* [WinRM](network-hacking/winrm.md)

## Post Exploitation

* [Windows](post-exploitation/untitled.md)
  * [CLI Tips](post-exploitation/untitled/cli-tips.md)
  * [Shells](post-exploitation/untitled/shells.md)
  * [Windows Script Host](post-exploitation/untitled/page-3.md)
  * [Windows Privilege Escalation](post-exploitation/untitled/page-1.md)
    * [Enumeration](post-exploitation/untitled/windows-privilege-escalation/enumeration.md)
    * [JuicyPotato/RottenPotato](post-exploitation/untitled/windows-privilege-escalation/juicypotato-rottenpotato.md)
    * [Kernel Exploits](post-exploitation/untitled/windows-privilege-escalation/kernel-exploits.md)
    * [Unquoted Service Paths](post-exploitation/untitled/windows-privilege-escalation/unquoted-service-paths.md)
  * [Active Directory](post-exploitation/untitled/active-directory.md)
  * [Dumping Passwords](post-exploitation/untitled/dumping-passwords.md)
  * [NTLM Hash Theft](post-exploitation/untitled/ntlm-hash-theft.md)
* [Linux](post-exploitation/linux/README.md)
  * [Port Forwarding](post-exploitation/linux/port-forwarding.md)
  * [Shells](post-exploitation/linux/shells.md)
  * [Linux Privilege Escalation](post-exploitation/linux/linux-privilege-escalation/README.md)
    * [Enumeration](post-exploitation/linux/linux-privilege-escalation/enumeration.md)
    * [SUID Bit](post-exploitation/linux/linux-privilege-escalation/suid-bit.md)
    * [Dot (.) In PATH](post-exploitation/linux/linux-privilege-escalation/dot-.-in-path.md)
    * [Escape From Restricted Shell](post-exploitation/linux/linux-privilege-escalation/escape-from-restricted-shell.md)
    * [Symlink Trickery](post-exploitation/linux/linux-privilege-escalation/symlink-trickery.md)
    * [Wildcard Injection](post-exploitation/linux/linux-privilege-escalation/wildcard-injection.md)
    * [Docker group/LXD group](post-exploitation/linux/linux-privilege-escalation/docker-group-lxd-group.md)
    * [Password Reuse](post-exploitation/linux/linux-privilege-escalation/password-reuse.md)
  * [Backdoors](post-exploitation/linux/backdoors.md)
* [General](post-exploitation/general.md)

## Blue Team

* [Untitled](blue-team/untitled.md)

## Various

* [CVEs](various/untitled.md)
* [SSH Agent Hijacking](various/ssh-agent-hijacking.md)
* [Password Cracking](various/password-cracking.md)
* [Crypto](various/crypto.md)
* [Non-Hacking](various/non-hacking.md)
* [Malware](various/page-1.md)

## Binary Exploitation

* [Resources](binary-exploitation/untitled.md)
* [Base Knowledge](binary-exploitation/base-knowledge.md)
* [Format String Exploits](binary-exploitation/format-string-exploits.md)
* [Stack Smashing](binary-exploitation/stack-smashing.md)

## Physical Security

* [Untitled](physical-security/untitled.md)

## Social Engineering

* [Phishing](social-engineering/phishing.md)
