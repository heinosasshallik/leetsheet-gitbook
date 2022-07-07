# Redis SSRF

{% embed url="https://www.youtube.com/watch?v=LrLJuyAdoAg" %}

It used to be that if you could make requests to Redis through [SSRF](redis-ssrf.md#undefined), you were able to get RCE. However, because Redis is aware that this is a big issue, they will terminate the connection when they come across a line starting with `POST` or `Host:`.&#x20;

So you need to somehow get text into Redis before the `Host:` line comes. One way to accomplish this is to use a CRLF injection. This might not work for HTTP SSRFs, but if you can use the `git://` protocol, for example, then it might work.

Example payload can be found here:&#x20;

{% embed url="https://gitlab.com/gitlab-org/gitlab-ce/issues/41293" %}
