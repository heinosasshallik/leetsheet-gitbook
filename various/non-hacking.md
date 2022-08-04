# Non-Hacking

## Keylogging Any Terminal Which Belongs To You

Can be used on hackthebox, for example, since you and other users frequently use the same terminal. You can also use it if you have high privileges, for example if you are root, and you want to spy on a different user's terminal.

If you run the `tty` command, then you’ll get something like `/dev/pts/14`. This tells you what your pty number is 14.

Assuming there is a user whose pty number is 15, and you have the privileges to read `/dev/pts/15`, then you can do `cat /dev/pts/15`, and you will receive (some part of, not all of) the input of user 15’s terminal.

If you do `echo hello > /dev/pts/15`, then you will write to his terminal.

Note that when you snatch a character from another user’s input, then it will not appear on his terminal. So you should echo back any characters you cat from him.

It seems the characters you manage to snatch/not to snatch are random (race condition). So possibly if you use more than one user for `cat`ing `/dev/pts/15`, then you will receive a larger percentage of the input

Note that this cannot be used to capture passwords, since the letters do not appear in the terminal window when typing out a password.

## Virtual Machine Setup

### VirtualBox

Settings -> network -> bridged or host-only adapter.\
You can see the range of the adapter in file->host network manager. It’s 192.168.56.1 by default.

#### Host Only

Connecting to the VM:\
Edit /etc/interfaces to make the ip static. Make the ip be in the same range as the adapter and set the gateway to the adapter

```
sudo nano /etc/network/interfaces

# Interfaces configuration
iface eth0 inet static
address 192.168.56.20
netmask 255.255.255.0
gateway 192.168.56.1

# Restart the interface
sudo ifdown eth0
sudo ifup eth0
```

#### Bridged

Make sure virtualbox is running a dchp service.

```
sudo nano /etc/network/interfaces

# interfaces file configuration
iface eth0 inet dhcp

# Restart the interface
sudo ifdown eth0
sudo ifup eth0
```

### Hyper-V

See what the gateway IP is by doing cmd -> ipconfig.

If you can ping 8.8.8.8 but not google.com, then you have no DNS.

```
nano resolv.conf

# resolv.conf configuration:
nameserver 8.8.8.8
```

## Resolving Linux Problems

### Linux Clock is Wrong

Update the clock:

```
sudo ntpdate -s time.nist.gov
```

## Steganography

Stego-toolkit is pretty good for CTF excercises.

{% embed url="https://github.com/DominicBreuker/stego-toolkit" %}

### Exif Data

Use exiftool to extract exif data. Sometimes it will tell you there's some extra encoded data you can extract. You can extract it or binwalk it

```
exiftool filename.jpg
```

If you extract something using the `-b` flag, then you can binwalk whatever you've extracted

### **Binwalk** F**or Embedded Files or Code**

Binwalk is a tool for searching binary images for embedded files and executable code. Super useful for finding whether an image contains extra files or code.

```
binwalk file.ext
```

You can extract the detected data using:

```
binwalk -e file.jpg 

```

Though, keep in mind that [it's normal for images to contain zlib compressed data.](https://security.stackexchange.com/questions/144530/what-to-do-with-output-files-from-binwalk/144593)

## OS Install

### Windows

A non-activated official version of Windows can be installed from Microsoft’s website. Use either windows’ own tool (didn’t work for me) or [Rufus](https://rufus.ie/en/) to install onto USB. Use a good USB that has at least 8GB space.

HWIDGEN is frequently used to **illegally** activate Windows for free.

## Persistent Kali

Use this guide

{% embed url="https://devanswers.co/guide-kali-linux-2018-live-usb-encrypted-persistence-windows/" %}

When writing `persistence.conf`, instead of following the instructions, go there with `cd` and write the file using `touch` and `nano`.

