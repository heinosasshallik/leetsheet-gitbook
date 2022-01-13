# JWT Attacks

A JSON Web token is a string with the format `header.payload.signature`. The signature is provided by the remote server, and it will verify that signature later, based on the **algorithm** specified in the header, to see if the contents of the payload can be trusted.&#x20;

The format of the JWT is:&#x20;

```
data = base64urlEncode(header) + '.' + base64urlEncode(payload)
hashedData = hash(data, secret)
signature = base64urlEncode(hashedData)
jwt = data + '.' + signature
```

_Note: In the above format, the `hash` function is specified in the header, in the `alg` variable. Example: HS256._

### Changing the algorithm to “none”

One of the most common vulnerabilities is forgetting to check that the algorithm is acceptable because a “none” algorithm also exists. When you test that, then leave the last dot there, but delete the signature part.

However, all the times I’ve tested this, the library knows to not allow the “none” algorithm. Still worth checking in case the JWT library is not mature, though.

### Changing the algorithm from RS256 to HS256

The algorithm HS256 uses a secret key to sign and verify each message. The algorithm RS256 uses a private key to sign messages, and a public key to verify them. If we change the algorithm from RS256 to HS256, the signature is now verified using the HS256 algorithm using the public key as the secret key. Since the public key is not secret at all, we can correctly sign such messages.

### Brute forcing the key

They might have also used a weak algorithm. Or they might have used a weak key. In that case, you can try to brute force the key.

### Timing attack

{% embed url="https://hackernoon.com/can-timing-attack-be-a-practical-security-threat-on-jwt-signature-ba3c8340dea9" %}

If the algorithm is poorly implemented, then a more correct signature will take longer to check than a less correct signature. Therefore, you can make requests and figure out the correct signature just by measuring the time it takes to get a response.
