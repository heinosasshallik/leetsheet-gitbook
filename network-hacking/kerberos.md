# Kerberos

## Brute Force/Enumeration



Enumerate usernames and passwords with kerbrute.

* Enumerating usernames **does not** result in accounts getting locked out
* Enumerating passwords **does** result in accounts getting locked out and counts against the lockout policy.&#x20;
* Stealthier because Kerberos pre-authentication **does not** trigger a traditional logon failure (4625) event. It has to be manually turned on and will be logged in a separate location.

Enumerating users from a wordlist (DC name and hostname is CONTROLLER.local):

```
./kerbrute userenum --dc CONTROLLER.local -d CONTROLLER.local wordlist.txt
```

## Kerberoasting

{% embed url="https://room362.com/post/2016/kerberoast-pt1/" %}

{% embed url="https://www.blackhillsinfosec.com/a-toast-to-kerberoast/" %}

When a domain account is configured to run a service in the environment, such as MS SQL, a Service Principal Name (SPN) is used in the domain to associate the service with a login account. When a user wishes to use the specific resource they receive a Kerberos ticket signed with the NTLM hash of the account that is running the service.

We can request that ticket with the NTLM hash, and then crack it using hashcat to gain access to the system.

Dump hashes for all kerberoastable accounts using [Rubeus](https://github.com/GhostPack/Rubeus) (has to be run from the compromised machine):

```
Rubeus.exe kerberoast
```

The same can be accomplished using Impacket’s GetUserSPNs.py, which you can also run from a remote machine. Note that you need the username and password of a compromised user (any user, doesn't have to have special permissions) in the active directory domain.

```
sudo python3 GetUserSPNs.py controller.local/Machine1:Password1 -dc-ip 10.10.135.235 -request
```

Then, save the hash and then crack it using a password wordlist (copying the hash from Rubeus might result in an error, but impacket should work):

```
hashcat -m 13100 -a 0 service.hash passwords.txt
```

Mitigation: use Managed Service Accounts instead of Domain Accounts

## AS-REP Roasting

If a user (not necessarily a ServiceUser) has pre-auth disabled, then they can be AS-REP roasted. It’s **not vulnerable by default**, though, and **finding this is uncommon**.

**You don't need to be authenticated to do AS-REP roasting.**

You can try to find users with pre-auth disabled using impacket**:**

```
python3 ~/tools/impacket/examples/GetNPUsers.py -dc-ip forest.local -request 'htb.local/'
```

**Make sure you have a slash after the domain name.**

* `-dc-ip` specifies the IP address or host of the domain controller
* `htb.local` was the domain I wanted to query

_Note: there is an `-usersfile` flag if you want to specify a "users file", but it will find users even without that flag._

You can then crack the hash (the whole line you get from the -request flag):

```
hashcat64 -m 18200 -a 0 "PASTE_THE_WHOLE_LINE_HERE" wordlist.txt
```

### How GetNPUsers Works

{% embed url="https://www.youtube.com/watch?v=pZSyGRjHNO4" %}

There's an attribute userAccountControl that Windows users have. It's a number that contains within itself some information about the user. Among that information is the setting of whether kerberos pre-auth is disabled or not.&#x20;

GetNPUsers does an LDAP search for this attribute. It finds any objects in the domain where the user account control is set to DONT\_REQUIRE\_PREAUTH, and where the account isn't disabled.

Once a suitable user account is found, if the -request flag is set, then it builds a kerberos request and gets an AS\_REP response. The AS\_REP contains the TGT. It's encrypted using the password hash, and can be brute forced.

Also, getNPUsers asks for an encryption of type eTYPE-ARCFOUR-HMAC-MD5, which is useful, because md5 is much weaker than the default encryption that kerberos uses.

Specifically, getNPUsers looks at the encrypted part (enc-part) of AS-REP, and looks at the cipher. That cipher is what we're cracking, because the cipher was encrypted using the user's password (or password hash?).

### Cause and Mitigation

When you do not enforce pre-authentication, a malicious attacker can directly send a dummy request for authentication. The KDC will return an encrypted TGT and the attacker can brute force it offline.

If pre-auth is enabled, then this attack is thwarted, because if you send an AS-REQ request, then you get an ERROR\_PREAUTH\_REQUIRED response.

If pre-auth is enabled, then the server is expecting us to encrypt the current time and send it with the request. The server will then decrypt it with the user's password (hash?). Since we don't know the user's password, then we can't send the preauth.&#x20;

The encrypted current time has to be sent along with the AS-REQ request in the padata section.

The time specifically is encrypted to prevent replay attacks. The time has to be in the same as the server's (with a margin of error), or else the server won't accept the request. The default acceptable time error might be around 5 minutes (?) in windows installations?
