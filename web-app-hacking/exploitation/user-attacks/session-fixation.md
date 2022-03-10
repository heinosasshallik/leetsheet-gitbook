# Session Fixation

Occurs when one person can set another person’s session token. In most basic case, this happens when session tokens are accepted in GET or POST data.

**Example Attack scenario**

An attacker gives the victim a link and the victim goes to it (`vulnerable.com/sid=I_GAVE_YOU_THIS_SID`). It prompts for a login. If on login, the victim has the session id `I_GAVE_YOU_THIS_SID`, then it’s bad. The attacker who gave the sid can log in with that session id.

When trying to execute this attack as an attacker, `I_GAVE_YOU_THIS_SID` should ideally be a server-generated session id (an expired session id that was generated for the attacker by the server) so you can be sure that it's in the correct format.

In a secure web application, the `I_GAVE_YOU_THIS_SID` token wouldn't be reused. Upon logging in, it would be thrown away and another token would be given instead.

### XSS + Session Fixation

If an application doesn't generate a new session token upon logging in but rather reuses the old one for logging in, then that's a session fixation vulnerability. In that case, you can facilitate the session fixation attack by using XSS to set the session token.

In this example, the token is stored in a cookie and XSS is used to set that cookie:

```
http://website.kom/<script>document.cookie=”sessionid=abcd”;</script>
http://website.kon/<meta http-equiv=Set-Cookie content=”sessionid=abcd”>
```

