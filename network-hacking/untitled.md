# General Enumeration

## SSH Version

If the machine allows SSH, then looking at the OpenSSH version will give you an idea of when the machine was last updated.&#x20;

Also, if the machine was never updated (like in HackTheBox), then you can match the release date of the OpenSSH version to a Linux version. For example, if the machine is an Ubuntu machine, then you can look at which version of Ubuntu was latest when that release of OpenSSH was latest.

## Port Scanning

Port scanning is an important part of enumerating the services that are running on a network machine.

### Nmap

Normal TCP scan:

```
nmap -sC -sV -p- -vvv hostname_here 
```

UDP scan &#x20;

```
nmap -sU -sC -sV -p- -vvv hostname_here
```

{% embed url="https://hackertarget.com/nmap-cheatsheet-a-quick-reference-guide/" %}

Common flags:

* `-p-` : Scan all ports
* `-vvv` : Maximum verbosity
* `-sV` : Service detection
* `-A` : Detect all things, including services and OS
* `-sC` : Scan using default **safe** scripts
* `-Pn` : Scan a host even if it doesn't respond to pings

Stealth scans:

{% embed url="https://nmap.org/bennieston-tutorial/" %}

Finding nmap scripts:

```
locate *.nse
```

## AutoRecon

Autorecon is a script for automating your network enumeration activities. It can save you a lot of time and make sure you don't forget to enumerate anything you should.

Installation:

```
sudo apt install python3-pip
sudo python3 -m pip install git+https://github.com/Tib3rius/AutoRecon.git
```

Simple usage:

```
sudo autorecon target_hostname
```

I have customized AutoRecon to my needs. I host my custom AutoRecon plugins [here](https://github.com/heinosasshallik/infosec-knowledge/tree/master/scripts/autorecon\_plugins). When I run AutoRecon, I separately scan for directories using a huge wordlist, and then scan for files with a smaller wordlist and a few manually selected file extensions:

```
sudo $(which autorecon) target_hostname \
  --single-target \     
  --output autorecon \
  --dirbuster.tool gobuster \
  --dirbuster.wordlist "/home/x90slide/resources/infosec-knowledge/wordlists/web_content/combined_directories.txt" \
  --dirbuster.ext "" \
  --dirbuster-manual-extensions.wordlist "/home/x90slide/resources/infosec-knowledge/wordlists/web_content/combined_words.txt"
```
