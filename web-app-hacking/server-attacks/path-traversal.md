# Path Traversal

List of interesting files you can try to read on a vulnerable machine when you have identified a path traversal vulnerability:

{% embed url="https://digi.ninja/blog/when_all_you_can_do_is_read.php" %}

### Tomcat Path Normalization Inconsistencies

{% embed url="https://www.acunetix.com/vulnerabilities/web/tomcat-path-traversal-via-reverse-proxy-mapping" %}

When you have a reverse proxy in front of Tomcat that denies access to the `/manager` endpoint, then it might still be able to access that page by exploiting path normalization inconsistencies between tomcat and the reverse proxy.

Tomcat will treat the sequence `/..;/` as `/../` . However,  reverse proxies such as Nginx will not normalize this sequence and send it to Tomcat as-is. This allows you to access paths that are otherwise denied by the reverse proxy.
