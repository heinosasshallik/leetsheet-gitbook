# Password Cracking

## Wordlist Generation

### Combinations Using Python

This is just a simple script for trying out all two word combinations of words in a list:

```
from itertools import combinations

lines = [ 'one', 'two', 'three' ]
strippedlines=[]
for line in lines:
  strippedlines.append(line.strip())

for combination in list(combinations(strippedlines, 2)):
  print('{}{}'.format(combination[0], combination[1]))
```

### Rules

You can use hashcat to generate a wordlist based on an existing wordlist and some rules. Here is an example with the bes64 ruleset:

```
hashcat --force initial_wordlist.txt -r /usr/share/hashcat/rules/best64.rule --stdout > rules_best64_wordlist.txt
```

**Note**: Ippsec uses the InsidePro-PasswordsPro.rule. That's probably a really good one.

## Cracking Tools

### Hate\_crack

Tool for automating/combining different types of offline password cracking methods.

{% embed url="https://github.com/trustedsec/hate_crack" %}

### Hashcat

Utilizes the GPU, which is good, as it cracks very fast.

```
hashcat -a 0 -m HASH_MODE -o output.txt input_hashes.txt wordlist.txt
```

Important attack modes (-a):

* 0: dictionary attack

Hash modes (-m):

* Look them up in the hashcat manual

You can crack hashes with rules applied to a wordlist:

```
hashcat -m HASH_MODE crackthis.hash  wordlist.txt -r rulesfile.txt --debug-mode=1 --debug-file=matched.
```
