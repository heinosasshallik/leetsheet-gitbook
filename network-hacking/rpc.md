# RPC

## Enumeration

### List Network Interfaces

{% embed url="https://airbus-cyber-security.com/the-oxid-resolver-part-1-remote-enumeration-of-network-interfaces-without-any-authentication/" %}

Use this script:

```
#!/usr/bin/python

import sys, getopt

from impacket.dcerpc.v5 import transport
from impacket.dcerpc.v5.rpcrt import RPC_C_AUTHN_LEVEL_NONE
from impacket.dcerpc.v5.dcomrt import IObjectExporter

def main(argv):

    try:
        opts, args = getopt.getopt(argv,"ht:",["target="])
    except getopt.GetoptError:
        print ('IOXIDResolver.py -t <target>')
        sys.exit(2)

    target_ip = ""

    for opt, arg in opts:
        if opt == '-h':
            print ('IOXIDResolver.py -t <target>')
            sys.exit()
        elif opt in ("-t", "--target"):
            target_ip = arg

    if target_ip == '':
            print ('IOXIDResolver.py -t <target>')
            sys.exit()

    authLevel = RPC_C_AUTHN_LEVEL_NONE

    stringBinding = r'ncacn_ip_tcp:%s' % target_ip
    rpctransport = transport.DCERPCTransportFactory(stringBinding)

    portmap = rpctransport.get_dce_rpc()
    portmap.set_auth_level(authLevel)
    portmap.connect()

    objExporter = IObjectExporter(portmap)
    bindings = objExporter.ServerAlive2()

    print ("[*] Retrieving network interface of " + target_ip)

    #NetworkAddr = bindings[0]['aNetworkAddr']
    for binding in bindings:
        NetworkAddr = binding['aNetworkAddr']
        print ("Address: " + NetworkAddr)

if __name__ == "__main__":
   main(sys.argv[1:])
```

Run the following command:

```
IOXIDResolver.py -t TARGET_IP_HERE
```

Example:

```
└─$ python3 exploit/ioxidresolver.py -t cascade.htb  
[*] Retrieving network interface of cascade.htb
Address: CASC-DC1
Address: 10.10.10.182
Address: dead:beef::90c2:d9a5:3998:f429
```

### Domain Users and Groups

These commands should be run from an rpcclient prompt.

Enumerate domain users:&#x20;

```
enumdomusers
```

Enumerate domain groups:&#x20;

```
enumdomgroups
```

Query Group Information and Group Membership (you'll get the RIDs from the previous enumdomgroups command):&#x20;

```
querygroup GROUP_RID querygroupmem GROUP_RID
```

Query Specific User Information (including computers) by RID.&#x20;

```
queryuser USER_RID
```

### Password Policy

Get the domain password policy, and get the password policy for a certain user:

![](https://lh3.googleusercontent.com/YmxbEm\_PQo4g2bL3C1zOmblzPrG5Q68rVai0QELpRoTaVeKFcOZpgKyg-6AyFjmeAOUd8kbajmDWp9ax-zo93YrwOFNW4zHDDJW67LlQI8AwWkhSr9t\_xTurrkNvOFELXi2\_0dYavSLkUzvWHw)



### Password Spraying

{% embed url="https://www.blackhillsinfosec.com/password-spraying-other-fun-with-rpcclient/" %}

## Null Session

If null sessions are allowed, then you can connect using rpcclient like this:&#x20;

```
rpcclient -U "" -N IP_ADDRESS_HERE
```
