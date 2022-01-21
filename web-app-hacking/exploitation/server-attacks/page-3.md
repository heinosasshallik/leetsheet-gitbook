# Unrestricted File Upload

Unrestricted File Upload is a security vulnerability where an attacker can upload arbitrary files with attacker-controlled content, potentially to arbitrary locations.

Unrestricted file upload may be used to get:

* Remote Code Execution
  * Especially in PHP and similar languages, since uploaded files may commonly be parsed by the server if navigated to it.
  * When the web application runs under root and you can use path traversal to specify the directory to upload to. In that case, upload a file to `/etc/cron.d` in the correct format and it will get executed.
* Cross-Site Scripting, if you can add or overwrite a file that contains HTML
* XML External Entities: If the website uses an insecure XML parser, then you might be able to exploit an XXE vulnerability by getting the insecure parser to parse a malicious XML file. In that case, the file upload vulnerability can be used to smuggle a malicious XML file onto the web server for exploitation.

## Bypass Mitigations

### Bypass MIME Type Check

If the MIME type is checked by the target application, then use Burp Suite to change the MIME type to the correct value.

### Bypass Image Validity Check

If the image is checked for validity using an image library, then you can still produce a valid image that has malicious data in embedded in it. This is useful in PHP applications, for example. If you can upload a `.php` file with PHP code embedded in it, then that might lead to RCE.

This can be done using `jhead`.&#x20;

{% embed url="https://phocean.net/2013/09/29/file-upload-vulnerabilities-appending-php-code-to-an-image.html" %}

First, clear the headers of an existing `myfile.jpg` file:

```
jhead -purejpg myfile.jpg
```

Add an EXIF comment and write PHP code there:

```
jhead -ce myfile.jpg
```

Example code:&#x20;

```
<?php echo "hi"; __halt_compiler();?>
```

_Note: The `__halt_compiler()` prevents the image bytes from getting executed._

__
