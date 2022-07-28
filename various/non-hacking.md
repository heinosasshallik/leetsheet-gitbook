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

\[+] VirtualBox

Settings -> network -> bridged or host-only adapter.\
You can see the range of the adapter in file->host network manager. It’s 192.168.56.1 by default.

\


\[+] General:

Connecting to the VM:\
Edit /etc/interfaces to make the ip static. Make the ip be in the same range as the adapter and set the gateway to the adapter

\


\---- Default configuration for VirtualBox ---

(\*) Host only

\
sudo nano /etc/network/interfaces\
iface eth0 inet static\
address 192.168.56.20\
netmask 255.255.255.0\
gateway 192.168.56.1\
sudo ifdown eth0\
sudo ifup eth0

\


(\*) Bridged

(make sure virtualbox is running a dchp service)

Sudo nano /etc/network/interfaces

iface eth0 inet dhcp

Sudo ifdown eth0

Sudo ifup eth0

\


\[+] Hyper-V:

See what the gateway IP is by doing cmd -> ipconfig

If you can ping 8.8.8.8 but not google.com, then you have no DNS.

\


Nano resolv.conf

Nameserver 8.8.8.8
