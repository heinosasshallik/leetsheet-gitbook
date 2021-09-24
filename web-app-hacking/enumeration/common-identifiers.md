# Common Identifiers

## Common Files

Look at:

* `robots.txt`
* `.well-known/apple-app-site-association`
  *  This is used by pretty much every website that has a corresponding Apple mobile app tied to it

## Headers

View HTTP headers to see if they tell you something.

For HTTP headers:

```text
netcat [ip or domain] [port]
GET / HTTP/1.1
Host: [ip or domain]
```

For HTTPS headers:

```text
openssl s_client -connect [ip or domain]:443
GET / HTTP/1.1
Host: [ip or domain]
```

If requests don't come back like they do in the browser \(e.g 403 instead of 404\), there might be a WAF \(web application firewall\) installed. In that case, mimic the browser and send a user-agent string and other parameters. 

_Tip: You can copy a request as a curl request from firefox's network tab._

Interesting Headers:

* X-Frame-Options 
  * Might prevent you from doing clickjacking attacks
* Content-Security-Policy
  * Can protect against some exploits, depending on security policy.

## Confirm Use of PHP

Taken from [this](https://www.php.net/manual/en/security.hiding.php) documentation about how to hide PHP usage.

### PHP Easter Eggs

If `expose_php` hasn't been set to off in the Apache conf file \(which also hides .php extensions\), then you can put this as an argument to get php info: `?=PHPB8B5F2A0-3C92-11d3-A3A9-4C7B08C10000` .  There are also [other](https://stackoverflow.com/questions/10458610/how-can-i-disable-phps-easter-egg-urls) easter eggs. Not sure if they've been disabled in any recent PHP versions.

The PHP session ID cookie's name defaults to "PHPSESSIONID".

The website might have "X-powered by PHP" in a HTTP response header.







Find out PHP version



\(all of these removed since PHP 5.5, I can't get them to work anymore\)

Either through php info above, or by identifying what logo it has

https://labs.detectify.com/2012/10/29/do-you-dare-to-show-your-php-easter-egg/





