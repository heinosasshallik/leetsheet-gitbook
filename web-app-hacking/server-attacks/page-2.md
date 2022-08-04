# Insecure Deserialization

## PHP

{% embed url="https://book.hacktricks.xyz/pentesting-web/deserialization#php" %}

You can use phpggc to generate payloads.

{% embed url="https://github.com/ambionics/phpggc" %}

## Deserialization via PHAR archive

[https://i.blackhat.com/us-18/Thu-August-9/us-18-Thomas-Its-A-PHP-Unserialization-Vulnerability-Jim-But-Not-As-We-Know-It.pdf](https://i.blackhat.com/us-18/Thu-August-9/us-18-Thomas-Its-A-PHP-Unserialization-Vulnerability-Jim-But-Not-As-We-Know-It.pdf)

If you can upload a file that is a valid PHAR:&#x20;

* Phar file&#x20;
* Tar file&#x20;
* Zip file&#x20;
* Image polyglot

Then if that file is opened with the `phar://` protocol, then insecure deserialization can occur.

So basically, to execute the attack, you need two things:&#x20;

1. Uploaded valid phar archive with malicious content&#x20;
2. Injection into a filesystem call, where you can specify the `phar://` protocol and open up the archive
