# Automated Directory Enumeration

## Wordlists

If you choose to use SecLists' raft-medium-words wordlist, then keep in mind that you will not find /cgi-bin/, it will only find /cgi-bin \(without the slash\). You can add the slash using the --add-slash flag, but then it won't find it without the slash… 



I've combined multiple wordlists into one massive wordlist. They're available at:

{% embed url="https://github.com/heinosasshallik/infosec-knowledge/tree/master/wordlists/web\_content" %}

I recommend running 2 separate dirbusts:

* Dirbust for files using the `combined_words.txt` wordlist and specifying all important extensions.
* Dirbust for directories using the `combined_directories.txt` wordlist.



This can be run automatically with [AutoRecon](https://github.com/Tib3rius/AutoRecon), for example.



## Gobuster

Files search:

```text
gobuster dir -u http://server-client -w /usr/share/dirb/wordlists/common.txt  -x .php,.html,.txt --discover-backup
```



Flags:

* `--discover-backup` : Upon finding a file, search for backup files
  * [Not working correctly at the moment](https://github.com/OJ/gobuster/issues/298).

_Note: If you specify -x, then don’t worry, it also includes files without file extension_





## wfuzz

Brute force directories/files using wfuzz

https://hydrasky.com/network-security/wfuzz-bruteforcing-web-applications/

```text
wfuzz -c -z file,/usr/share/wfuzz/wordlist/general/common.txt --hc 404  http://vulnerable/FUZZ
```

Flags:

* `-s` : Time delay \(in seconds\)
* `--hh` : Filter out character length
* `--hc` : Filter out status codes
* `-R10` : Sets recursion with a depth of 10
  * Be wary of HTTP Forbidden headers





