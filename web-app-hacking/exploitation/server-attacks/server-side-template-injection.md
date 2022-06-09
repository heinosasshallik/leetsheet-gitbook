# Server-Side Template Injection

{% embed url="https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection" %}

Different template engines use different syntaxes. Try to identify the type of template engine used with payloads such as these:

```
{{7*7}}
${7*7}
<%= 7*7 %>
${{7*7}}
#{7*7}
```

If the result is 49, then you know what the syntax is. From there, try to identify the specific template engine used and see if there's an exploit you can use for that specific template engine.

_Note: When reading the SSTI HackTricks article, then keep in mind that it doesn't seem to list the vulnerable template engine versions. For example, the Handlebars.js exploit listed there is patched in newer versions. Also, even in older versions, at least when I tried it, the exploit shown there didn't work, and you had to use a_ [_workaround_](https://licenciaparahackear.github.io/en/posts/bypassing-a-restrictive-js-sandbox/) _to get it working (`require()` wasn't loaded)._
