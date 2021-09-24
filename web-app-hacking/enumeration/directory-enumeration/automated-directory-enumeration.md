# Automated Directory Enumeration

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





