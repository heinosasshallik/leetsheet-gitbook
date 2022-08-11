# RPC

## Enumeration

If you've got an rpcclient prompt, then you can use it for enumeration.&#x20;

{% embed url="https://www.blackhillsinfosec.com/password-spraying-other-fun-with-rpcclient/" %}

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
