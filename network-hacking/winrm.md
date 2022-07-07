# WinRM

WinRM is a Windows remote management tool that runs on port 5985. If you have credentials to a user, then you can use this to get a shell:

```
gem install evil-winrm
evil-winrm -i IP_ADDRESS -u USER -p PASSWORD
```

{% embed url="https://github.com/Hackplayers/evil-winrm" %}
