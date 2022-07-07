# Phishing

## Homoglyphs

{% embed url="https://www.offensity.com/de/blog/sophisticated-spear-phishing-campaigns-using-homograph-attacks/" %}

Homoglyphs are Unicode characters that look visually similar to an ASCII character, but are different. You can use these to make your phishing attacks more convincing.

Note: Gmail shows a warning when this is used, but not all email providers do.

![](https://lh6.googleusercontent.com/ef5s5wTgrmWo9Vut2YzyGBmJ4OeVEuf3eMy5k8RvaDqgzES\_WXX1FKHFKUL4TMSf6\_fWinpw8GWeXGCKk71Be\_uN5YPNuKCo\_KssRfPmfO5aYzxo\_S3RUaSit0IVUuYu6aEW7E56lh1pYNOUhA)

Also, you can register a domain with a homoglyph and direct users there.

## Fake Window

{% embed url="https://pentesttools.net/warning-new-phishing-attack-that-even-most-vigilant-users-could-fall-for/" %}

Using Javascript, you can make a fake window that looks exactly like Facebook and that asks you for the login (for OAuth logins).

## Reverse Tabnabbing

{% embed url="https://owasp.org/www-community/attacks/Reverse_Tabnabbing" %}

If a website has a link like this:

```
<li>
    <a href="bad.example.com" target="_blank">
        Vulnerable target using html link to open the new page
    </a>
</li>
```

\
Or like this:

```
<button onclick="window.open('https://bad.example.com')">
    Vulnerable target using javascript to open the new page
</button>
```



Then it’s vulnerable to reverse tabnabbing (tested 23 May 2019 on Firefox and Chrome).

_Note: `target="_blank"` is used to get the link to open in a new tab._

When you have `target=`"`_blank"`, then you should also really have `rel=`"`noopener noreferrer"` next to it. Otherwise, `bad.example.com` will have the `window.opener` object available to it.\
\
If the website `bad.example.com` runs this Javascript:

```
window.opener.location = "https://phish.example.com";
```

Then the **original tab** will be redirected to a phishing site.

Example: Facebook lets you link to your site using `target="_blank"`. On your site, you run the above Javascript and the original Facebook tab will be redirected to https://phish.example.com. Assuming you control that domain, you can have it be a phishing site that asks the user to re-enter their password, or something similar.

## Spear Phishing

{% embed url="http://blog.cobaltstrike.com/2015/09/30/advanced-threat-tactics-course-and-notes/" %}

Targeted attacks:

{% embed url="https://youtu.be/CxQfWtqpwRs" %}

## Email Spoofing

One way to do this is via open relay servers, but those might get blacklisted and there’s a better alternative:

Buy a domain (or use a free one that allows emails to be sent, like 000webhostapp) and create a PHP script that allows you to send emails with custom SMTP headers.&#x20;

This works after changing the form action in index.php:

{% embed url="https://github.com/ShubhamBadal/email-spoofer" %}

_Note: the script doesn't accept unicode._

Hosted at [http://oger55.000webhostapp.com/spoofer/](http://oger55.000webhostapp.com/spoofer/)
