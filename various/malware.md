# Malware

## Analysis

### Microsoft OLE2 Files&#x20;

OLE2 is the format for Microsoft Office files. Use oletools to find macros and other things inside OLE files:

{% embed url="https://github.com/decalage2/oletools/" %}

### Online Sandboxes

For detecting/reversing malware try these online sandboxes:

* [www.hybrid-analysis.com](http://www.hybrid-analysis.com)
* [www.reverse.it](http://www.reverse.it)
* [https://cuckoosandbox.org/](https://cuckoosandbox.org/)

## Creation

### Evading Antivirus

For hiding your executable from AV, shellter is better than msfvenom. Also you can use Veil along with iexpress.exe

You can use PS2EXE to convert a powershell script to an executable - makes it easy to download a payload from the internet and execute it.

Meta-twin is a tool that copies the metadata (including the signature, though it will no longer be valid) from an application to your payload. For example, before using this tool, 95% of antiviruses detected the PS2EXE executable as malware. After using this tool, the number dropped significantly (for example windows defender couldnt detect anymore)

Invoke-obfuscation is a powershell command obfuscator.

### Persistence

To have persistence on a machine, you could use WMI-persistence from github. It uses WMI events for fileless persistence

## Drop Vectors

### Windows Settings Shortcut RCE

June 2018 - getting a victim to download and execute a Windows Settings Shortcut file leads to RCE. This can be placed in an Office file, as it’s new and thus not in the blacklist (it is, however, blocked from Microsoft office365 since 11. July 2018).

{% embed url="https://www.bleepingcomputer.com/news/security/windows-settings-shortcuts-can-be-abused-for-code-execution-on-windows-10/" %}

